# 25: Real-World Data Feeds for the time.cell

The `time.cell` for paper trading requires a sequenced input of historical price data. This document describes the three implemented data feeds designed to provide this input, adhering to a consistent iterator contract. This contract ensures the `PaperTrader` component, along with the `TimeCell` machinery, `forecast_trend`, and `TradingDecisionSupport` modules, remains decoupled from the data source.

## The Iterator Contract

All data feeds conform to an iterator contract, yielding `(timestamp_ms, price)` tuples.
*   `timestamp_ms`: An integer representing milliseconds since the Unix epoch.
*   `price`: A floating-point number representing the asset's price at that timestamp.

This contract provides a stable abstraction layer. The downstream `PaperTrader` consumes this sequence without needing knowledge of the data's origin, format, or retrieval mechanism. This modularity facilitates independent development and testing of feed implementations and trading logic.

## CSVPriceFeed

The `CSVPriceFeed` reads price data from a local or remote CSV file. This feed is designed for scenarios where historical data is available in a common delimited format.

### Implementation Details

*   **Dependency-free parsing:** The feed utilizes Python's standard `csv.reader` module. It explicitly avoids external dependencies like `pandas` or `numpy.genfromtxt`, minimizing the distribution footprint.
*   **Date Parsing:** Date and time columns are identified and parsed using `datetime.strptime`. To enhance robustness, `CSVPriceFeed` implements a fallback mechanism, attempting to parse date strings against a predefined list of common formats (e.g., `YYYY-MM-DD`, `MM/DD/YYYY`, `MM-DD-YYYY`, `YYYY/MM/DD`). The first format that successfully parses a date in the header row is adopted for the entire file.
*   **Column Mapping:** The feed expects two columns: one identifiable as a date/timestamp and another as a price.
*   **Verification:** `CSVPriceFeed` has been verified using 500 days of synthetic data shaped like Apple Inc. (AAPL) stock and on actual historical AAPL data retrieved from Yahoo Finance.

### Example Usage (Internal)

```python
import csv
from datetime import datetime

class CSVPriceFeed:
    def __init__(self, filepath, date_col='Date', price_col='Close'):
        self.filepath = filepath
        self.date_col = date_col
        self.price_col = price_col
        self._date_formats = [
            "%Y-%m-%d", "%m/%d/%Y", "%m-%d-%Y", "%Y/%m/%d",
            # Add more formats as needed for robustness
        ]
        self._parser = None

    def _determine_date_parser(self, header):
        date_idx = header.index(self.date_col)
        with open(self.filepath, 'r') as f:
            reader = csv.reader(f)
            next(reader) # Skip header
            for row in reader:
                sample_date_str = row[date_idx]
                for fmt in self._date_formats:
                    try:
                        datetime.strptime(sample_date_str, fmt)
                        self._parser = lambda s: int(datetime.strptime(s, fmt).timestamp() * 1000)
                        return
                    except ValueError:
                        continue
                raise ValueError(f"Could not determine date format for '{sample_date_str}'")
        
    def __iter__(self):
        with open(self.filepath, 'r') as f:
            reader = csv.reader(f)
            header = next(reader)
            self._determine_date_parser(header)
            
            date_idx = header.index(self.date_col)
            price_idx = header.index(self.price_col)
            
            for row in reader:
                timestamp_ms = self._parser(row[date_idx])
                price = float(row[price_idx])
                yield timestamp_ms, price
```

## YahooFinanceFeed

The `YahooFinanceFeed` retrieves real-time and historical price data directly from Yahoo Finance's public API.

### Implementation Details

*   **Direct API Access:** This feed interacts with the `v8 chart API` endpoint at `query1.finance.yahoo.com`.
*   **No External Dependencies:** Data retrieval is accomplished using Python's standard `urllib` module for HTTP requests and `json` for parsing the API response. There is no reliance on third-party libraries like `yfinance`.
*   **Authentication:** The Yahoo Finance v8 chart API does not require authentication or an API key for public data access.
*   **Data Fields:** The feed extracts `timestamp` and `close` price data from the API response.

### Example Usage (Internal)

```python
import urllib.request
import json

class YahooFinanceFeed:
    def __init__(self, ticker, start_date_unix_s, end_date_unix_s):
        self.ticker = ticker
        self.start_date = start_date_unix_s
        self.end_date = end_date_unix_s
        self._api_url_base = "https://query1.finance.yahoo.com/v8/finance/chart/"

    def __iter__(self):
        url = (
            f"{self._api_url_base}{self.ticker}"
            f"?period1={self.start_date}&period2={self.end_date}"
            "&interval=1d&events=history"
        )
        
        with urllib.request.urlopen(url) as response:
            data = json.loads(response.read().decode())
            
        chart = data['chart']['result'][0]
        timestamps = chart['timestamp']
        prices = chart['indicators']['quote'][0]['close']
        
        for i in range(len(timestamps)):
            if prices[i] is not None: # Filter out null prices (e.g., non-trading days)
                yield int(timestamps[i] * 1000), float(prices[i])
```

## RandomWalkFeed

The `RandomWalkFeed` generates a deterministic sequence of prices based on a random walk algorithm.

### Implementation Details

*   **Unit Testing:** This feed is primarily used for unit tests and reproducible simulations. Its deterministic nature ensures that test cases produce identical results across multiple executions.
*   **Seed Control:** The walk's sequence is controlled by a specified random seed. Providing the same seed will always generate the identical price sequence.
*   **Configuration:** Parameters such as initial price, volatility, and number of steps can be configured.

### Example Usage (Internal)

```python
import random

class RandomWalkFeed:
    def __init__(self, seed, initial_price, num_steps, shock_magnitude=0.01):
        self.seed = seed
        self.initial_price = initial_price
        self.num_steps = num_steps
        self.shock_magnitude = shock_magnitude

    def __iter__(self):
        random.seed(self.seed)
        current_price = self.initial_price
        current_timestamp = 1672531200000 # Jan 1, 2023, 00:00:00 UTC in ms

        for _ in range(self.num_steps):
            yield current_timestamp, current_price
            
            # Simple multiplicative random walk
            change = 1 + (random.uniform(-self.shock_magnitude, self.shock_magnitude))
            current_price *= change
            current_timestamp += 86400000 # Advance by one day (in ms)
```

## Command-Line Interface (CLI)

The command-line interface for the `time.cell` allows users to select and configure the data feed.

*   `--csv <filepath>`: Activates `CSVPriceFeed` and specifies the path to the CSV file.
*   `--ticker <symbol>`: Activates `YahooFinanceFeed` for the specified stock symbol.
*   `--start <YYYY-MM-DD>`: Sets the start date for `YahooFinanceFeed`.
*   `--end <YYYY-MM-DD>`: Sets the end date for `YahooFinanceFeed`.
*   `--shock <magnitude>`: Configures the `RandomWalkFeed` with a specific price shock magnitude, implying its activation for testing or specific simulation scenarios.

Only one data feed can be active at a time; specifying conflicting options will result in an error or precedence rule application.

## `quf://` URI Scheme for Trade Logs

All paper trading sessions generate a log of executed trades. These logs are stored using the `quf://` URI scheme. This scheme allows the trade log to be version-controlled and CRDT-mergeable. Specifically, the `quf://` URI links the trade log to the specific data feed and configuration that generated it, enabling the system to track the context of trading decisions and facilitating the merging of logs generated from divergent data sources or parameters into a consistent history. For example, `quf://<feed_type>/<feed_identifier>/<start_date>/<end_date>/<session_id>.log` might uniquely identify a log.

## Verification and Testing

The robustness of these data feeds and their integration into the `PaperTrader` has been verified through a suite of 27 dedicated paper-trader tests. These tests cover scenarios such as:
*   Correct parsing of various CSV date formats.
*   Accurate retrieval of historical data from Yahoo Finance within specified date ranges.
*   Reproducibility of price sequences from `RandomWalkFeed` given a fixed seed.
*   Error handling for malformed input or network issues.
*   Ensuring the `PaperTrader` correctly processes the `(timestamp_ms, price)` tuples from all feed types.

## See also

*   [12: The TimeCell Architecture](12_time_cell_architecture.md)
*   [18: TradingDecisionSupport Module](18_trading_decision_support.md)
*   [Quilt Filesystem (QFS) Specification](qfs_spec.md)
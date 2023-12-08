# Portfolio Optimization with isyatirimhisse

This Python script utilizes the `isyatirimhisse` library to fetch historical stock data, calculates log returns, and performs a portfolio optimization using Monte Carlo simulation to find the maximum Sharpe ratio portfolio.

## Installation

To use this code, you need to install the `isyatirimhisse` library. You can install it using pip:

```bash
pip install isyatirimhisse==4.0.0
```

## Usage

### 1. Download Stock Data

You can download historical stock data for a list of symbols using the `download_stock_data` function. The example below fetches data for 500 days starting from '24-07-2020':

```python
from datetime import datetime
import pandas as pd

df = pd.read_excel('Sirketler.xlsx')
symbols = df['Kod'].tolist()
data = download_stock_data(symbols, start_date='24-07-2020', days_to_fetch=500)
```

### 2. Portfolio Optimization

The script then performs portfolio optimization using Monte Carlo simulation. It calculates the maximum Sharpe ratio portfolio and displays the results:

```python
returns, volatility, sharpe, max_sharpe, selected_stocks, selected_weights, max_sharpe_return, max_sharpe_vol = optimize_portfolio(log_returns, days=252)

result = (
    f"Maximum Sharpe Ratio: {max_sharpe:.4f}\n"
    f"Stocks and Weights of the Portfolio with Maximum Sharpe Ratio:\n"
)

for stock, weight in zip(selected_stocks, selected_weights):
    result += f"{stock}: {weight * 100:.2f}%\n"

result += (
    f"Return of the Portfolio with Maximum Sharpe Ratio: {max_sharpe_return * 100:.2f}%\n"
    f"Volatility of the Portfolio with Maximum Sharpe Ratio: {max_sharpe_vol * 100:.2f}%"
)

print(result)
```

### 3. Visualization

Finally, the script visualizes the portfolios in a scatter plot, with the color indicating the Sharpe ratio. The maximum Sharpe ratio portfolio is highlighted in red:

```python
plt.figure(figsize=(12, 8))
scatter = plt.scatter(volatility, returns, c=sharpe, cmap='viridis')
plt.colorbar(scatter, label='Sharpe Ratio')
plt.xlabel('Volatility')
plt.ylabel('Return')
plt.scatter(max_sharpe_vol, max_sharpe_return, c='red', s=50)
plt.show()
```

Feel free to customize the parameters and integrate this script into your financial analysis workflow.

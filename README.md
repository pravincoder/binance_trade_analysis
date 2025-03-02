# Binance Trade Analysis

## Overview
This project analyzes Binance trade data to rank accounts based on key financial metrics. The approach involves parsing trade history, extracting relevant features, computing financial metrics, and ranking accounts based on a weighted scoring system.

## Data Processing Steps
1. **Load Data**: The CSV file containing trade data is loaded into a Pandas DataFrame.
2. **Data Exploration**:
   - Display basic information about the dataset.
   - Preview initial rows.
3. **Data Cleaning**:
   - Convert timestamps to a readable datetime format.
   - Handle missing values by filling them with zeros.
4. **Extract Trade History**:
   - Parse the `Trade_History` column to extract individual trades.
   - Create a new DataFrame where each trade is a separate row.
   - Extract key details: `time`, `symbol`, `price`, `quantity`, `trade_type`, and `Profit/Loss`.

## Financial Metrics Computation
For each account (`Port_IDs`):
1. **Total Positions**: Number of trades executed.
2. **Winning Positions**: Number of trades with a positive profit.
3. **Win Rate**: Ratio of winning positions to total positions.
4. **Total Profit/Loss**: Sum of all realized profits/losses.
5. **Return on Investment (ROI)**:
   \[ ROI = \frac{Total Profit}{Total Investment} \]
6. **Sharpe Ratio**: Measures risk-adjusted returns.
   - Calculated using the mean and standard deviation of percentage changes in profit/loss.
7. **Maximum Drawdown (MDD)**: Measures the largest drop from peak to lowest point in cumulative profits.

## Ranking Algorithm
A weighted scoring system ranks the accounts:
\[ Score = (ROI \times 0.4) + (PnL \times 0.3) + (Sharpe Ratio \times 0.2) + (Win Rate \times 0.1) \]

- **ROI (40%)**: Prioritizes high returns relative to investment.
- **PnL (30%)**: Considers absolute profitability.
- **Sharpe Ratio (20%)**: Rewards stable, risk-adjusted gains.
- **Win Rate (10%)**: Provides a minor boost for consistent winning trades.

## Output
1. **calculated_metrics.csv**: Contains all computed metrics for each account.
2. **top_20_accounts.csv**: Ranks the top 20 accounts based on the weighted score.
3. **analysis_report.txt**: A summary report of the analysis.
4. **trade.csv**(optional) : All the trades row by row and imp params in each columns 

## Execution
1. Click on "Manual_ranking.ipynb"
2. Click on the colab notebook button
3. In Colab navbar options click on runtime , "Rull all cells"
4. Scroll at the bottom to see the final report and file section to access the "Top 20 accounts" and other csv.

## Future Enhancements
- Use **machine learning models** to predict profitable accounts.
- Implement **deep learning** for pattern recognition in trade history.
- Optimize scoring weights dynamically based on market conditions.

This analysis provides valuable insights into trading performance and helps in identifying top-performing accounts based on multiple financial metrics.


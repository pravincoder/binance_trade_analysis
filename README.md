# Task Description:

Dataset Information: You'll analyze historical trade data from various Binance accounts over 90 days, containing:

Port_IDs: Unique identifiers for accounts.
Trade_History: Historical trades with details like timestamp, asset, side (BUY/SELL), price, and more.
Objective: Analyze the dataset to calculate financial metrics for each account, rank them, and provide a top 20 list.

Metrics to Calculate:

ROI (Return on Investment)
PnL (Profit and Loss)
Sharpe Ratio
MDD (Maximum Drawdown)
Win Rate
Win Positions
Total Positions
Steps to Complete the Task:

Data Exploration and Cleaning:

Load and inspect the dataset, handle missing values.
Feature Engineering:

Determine feature importance and create a scoring system with weighted scores.
Ranking Algorithm:

Develop an algorithm to rank accounts based on calculated metrics.
Documentation:

Provide a concise report on methodology, findings, and assumptions.
Deliverables:

Jupyter Notebook or Python script with complete analysis and code.
CSV file containing calculated metrics.
List of top 20 accounts based on ranking.
Report detailing approach and findings.
Additional Information:

Win Positions: Number of profitable positions.
Position Identification:
Combine side and positionSide to classify trades (e.g., long_open, long_close).
quantity indicates money in the trade, qty indicates coin amount.
realizedProfit indicates profit or loss (depending on sign).
This task demands comprehensive data analysis to derive insights and rank accounts based on performance.
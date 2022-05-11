# Automatic-Report-Reader
## Description
Automate the reading of Financial Reports. Create a script to automatically retrieve financial results from publically listed companies on the stock market to give each company a score, and order/filter companies by score.

Meant to serve as a means to quickly filter out good companies and opportunities in the market during earnings season, and help an investor find strong positions and companies to research further, quickly.

Focused on US Equities.
## Automate retrival of Financial Reports
### Key Documents
Need to find some way to retrieve the following financial reports, extract the text and accounting data, and store into easily processed formats:
1. 10-K
2. 8-Q

Both documents can likely be retrived from the SEC, or from the company's official website.

### Tracking Companies
Need to automate the maintenance of a list of companies to track. The following indicies may serve as guidelines:
1. NDX
2. S&P500
3. Sector Select Indices by S&P Global

Since companies may be added or removed from indicies (For example, Macy's was removed from the S&P500 in 2020), will also need to program a logic to update list of companies to track/retrieve reports from.

In addition, we need to find a way to tell the computer when to download the earnings data. This will require getting a copy of the earnings release calendar from somewhere, and then programming the script to run the download and data processing functions at the date of release.

### Extracting Data
Need to find a way to pull out the string and floating point data from the downloaded format (Likely PDF) and export it into Python for data analysis.

## Rating Companies
How do we rate/filter companies based on their performance?

### Financials
Collect the following data/ratio from the Accounting declarations of the company:

INCOME STATEMENT
1. Gross Margin [Gross Profit/Revenue] (Higher is better)
2. Selling and General Administration costs (Lower is better, as a proportion of revenue)
3. R&D expenditures (Lower is better, as a proportion of revenue)
4. Depreciation (Lower is better, as a proportion of revenue)
5. Interest Expenses (Lower is better. Increasing trend is a red flag)
6. Net return [Net Profit/Revenue] (Higher is better)
7. Tax Provision (Must be around 20%)
8. Earnings Per Share [Net earnings/Outstanding Shares] (Higher the better, increasing trend is good)

BALANCE SHEET [ASSETS]
1. Assets must equal Liabilities and Shareholder Equity
2. Current Asset to total Asset ratio [Current Assets/Total Assets] (High Liquidity)
3. Trailing Change in Current Asset ratio (Liquidity Trend, must be growing or consistent)
4. Consistent growth or stable levels of inventory (Healthy growth in sales, or healthy demand for goods)
5. Net Receivables as a percentage of gross sales (If lower than competitors, better)

BALANCE SHEET [LIABILITIES]
1. Short term debt as a ratio of long term debt [Lower is better]
2. Long Term Debt due (under current liabilities, due the current year) [Low and consistent, no sudden spikes, no outliers]
3. Long Term Debt (Under non-current liabilities) to Net Profits ratio [How many years it takes to pay off all debt. Should be low.]
4. Low Shareholder Equity to Total Liability Ratio


### Normalising within Sectors
It is hard to optimise this problem. Ideally, we would have an output dataset to tune the variables listed above to train the model. However, it is not feasible to get this dataset. It would take too much time to read these reports and grade these companies based on their investability, and it would be difficult to find the correct people to grade these companies. It would not make sense to use the market cap of companies as a substitute either, since the free market is not efficient, and prices of businesses can vary irrationally. 

To manage this, we could use Borda Counting to rank companies of the same sector, and then return the companies in order of their Borda Score. The normalisation across sectors is required as different businesses may have different financial trends. For example, Banks will have high levels of liabilities, and industrial companies will have higher levels of R&D spending and Capital Expenditures.

### Normalising between Sectors
After Normalising within sectors, we can normalise between sectors. This is to control for market dominance. Companies that perform much better within their sector are more desirable. To normalise between sectors, we take their relative Borda Score within their sector and store that as a weight. For example, a company with a Borda Score of 10 in a sector with a summed Borda score of 100 will have a weight of (10/100) = 0.1. Their final Borda score will be 10 * 0.1 = 1.

The final Borda scores of the companies will then be sorted in increasing Borda Score, with the best companies having the lowest Borda Scores at the top.

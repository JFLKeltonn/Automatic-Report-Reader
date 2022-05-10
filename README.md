# Automatic-Report-Reader

## Description
Using NLP to Automate the reading of Financial Reports. Create a Software to automatically retrieve financial results from publically listed companies on the stock market, process the text data provided by the company management (Unstructured Data, NLP), as well as the accounting data (process numerical data), to classify companies into "Good Companies", "Troubled Companies" and "Weak Companies". Alternatively, give each company a score, and order/filter companies by score.

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


### Text Data


### Normalising against competitors



###

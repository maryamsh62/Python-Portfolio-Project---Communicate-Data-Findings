# Loan Data From Prosper Marketplace Exploration



## Dataset

### Prosper Marketplace Loan Data – Exploratory Data Analysis

> [Prosper Marketplace](https://en.wikipedia.org/wiki/Prosper_Marketplace), Inc. was founded in 2005 as the first peer-to-peer lending marketplace in San Francisco, California.
Through Prosper, people can invest in one another in ways that are both financially and socially rewarding. Borrowers apply online for a fixed-rate, fixed-term loan between 2,000 and 40,000 dollars. Individuals and institutions can invest in the loans and earn attractive returns. Prosper services all loans on behalf of the matched borrowers and investors. Prosper Marketplace is backed by leading investors, including Sequoia Capital, Francisco Partners, Institutional Venture Partners, and Credit Suisse NEXT Fund (accessed on 11/11/2020, source: https://www.prosper.com/about).

A small subset of the original Prosper data was selected for exploration. The cleaned subset (df_sub_clean) contains **14 columns** and **83,982 rows**. The columns are:


- ListingKey

- ListingCreationDate

- Term

- LoanStatus

- BorrowerAPR

- ProsperRating (numeric)

- ListingCategory (numeric)

- EmploymentStatus

- CreditScoreRangeLower

- InquiriesLast6Months

- IncomeRange

- StatedMonthlyIncome

- MonthlyLoanPayment

- Year_listingCreation (a derived column containing the year extracted from ListingCreationDate)



## Data Wrangling Process

**1. Gathering**

- Download the CSV file (prosperLoanData.csv).

- Load it into a pandas DataFrame.

**2. Assessing**

Inspecting the data visually and programmatically.

**Quality issues identified:**

- Convert ListingCreationDate from object to datetime.

- Convert Term to a categorical variable.

- Drop rows with null values in: CreditScoreRangeLower, InquiriesLast6Months, and ProsperRating (numeric).

- Convert CreditScoreRangeLower, InquiriesLast6Months, and ProsperRating (numeric) from float to integer.

- Extract the year from ListingCreationDate and store it in a new column (Year_listingCreation) for easier exploration.

- Convert the new year column to categorical.

- Convert ListingCategory (numeric) to categorical.

- Drop duplicates.

**3. Cleaning**

- Apply the fixes above and perform the analysis on the cleaned DataFrame (df_sub_clean).



## Summary of Findings


### Univariate Findings


- The majority of loans were listed in 2013 and had a LoanStatus of “Current.”

- Most employed borrowers with income ranges of 50,000–74,999 and 25,000–49,999 dollars applied for 36-month loans, and many of these loans were for Debt Consolidation.


### Bivariate Findings


- Borrower APRs were relatively high in 2011 and lower in 2014.

- As credit score increases and recent inquiries decrease, Prosper Rating increases and APR decreases.

- The lowest APRs belong to borrowers with an IncomeRange ≥ 100,000 dollars, followed by 75,000–99,999 dollars, especially for loans with a Current status.

- Borrowers with charged-off and defaulted loan status tend to have higher APRs.

- Loans with Current and Completed status generally have higher credit scores.

- From 2009–2011, most loans were Completed; from 2012–2014, most were Current.


### Multivariate Findings


- The average Borrower APR by loan status from 2009–2014 shows that Charged-off loans consistently have the highest APRs. APRs peaked around 2011 for all loan statuses and declined afterward.

- 12-month loans: Current and Defaulted loans tend to have higher Prosper Ratings. Most loans were completed, taken by borrowers earning 50,000–74,999, 100,000+, and 25,000–49,999 dollars, mainly for Debt Consolidation, followed by Other, Home Improvement, Business, Auto, and Household Expenses.

- 36-month loans: Current and charged-off loans show higher Prosper Ratings, and 36-month loans have a wider distribution overall. Most loans are Current, especially for income ranges of 50,000–74,999 and 25,000–49,999 dollars, and were mainly for Debt Consolidation and Other.

- 60-month loans: Completed, Charged-off, and Defaulted loans have similar Prosper Rating distributions. Most loans are Current for borrowers earning 50,000–74,999 and 25,000–49,999 dollars, again mostly for Debt Consolidation.

- A plot of APR vs. InquiriesLast6Months for Completed vs. Defaulted loans shows that Defaulted loans often have fewer inquiries but higher APRs.

- A plot of APR vs. CreditScoreRangeLower for Completed vs. Defaulted loans shows that:

  - Defaulted loans tend to have lower credit scores and higher APRs.

  - For both groups, lower credit scores correspond to higher APRs.

  - As the credit score increases, the APR generally decreases.

- From 2009 to 2014, Full-time and Retired borrowers had the lowest APRs. APRs decreased over time for Employed and Other borrowers, but increased for non-employed borrowers, peaking in 2013.

- In 12-month loans, Full-time borrowers had higher Prosper Ratings. Most employed borrowers in the 50,000–74,999 and 100,000+ dollar ranges applied for Debt Consolidation and Business loans.

- In 36-month loans, borrowers with Other employment status had lower Prosper Ratings. Employed, Self-employed, and not employed borrowers had higher Prosper Ratings (with different skews). Most employed borrowers earning 50,000–74,999 dollars took loans for Debt Consolidation.

- In 60-month loans, Retired borrowers had the highest Prosper Ratings. Most employed borrowers earning 50,000–74,999 dollars still borrowed for Debt Consolidation.

- Comparing employed vs. non-employed borrowers:

  - APR vs. InquiriesLast6Months: Not employed borrowers had fewer inquiries but higher APRs.

  - APR vs. CreditScoreRangeLower: Not employed borrowers tended to have higher APRs and lower credit scores, and for many of them, the APR did not decrease as the credit score increased.



## Key Takeaways

- Borrowers with **better credit indicators** (higher credit score, fewer recent inquiries, higher income) receive **lower APRs** and **higher Prosper Ratings**.

- **Debt Consolidation** is the dominant loan purpose across terms and income levels.

- **Loan status** is strongly associated with **APR** and **credit score** — worse outcomes (Chargedoff, Defaulted) are linked to higher APRs and lower scores.

- There is a clear time component: listings increased a lot in 2013, and APRs generally declined after 2011, suggesting changing platform risk/pricing over time.



## Resources

- https://www.prosper.com/
- https://en.wikipedia.org/wiki/Prosper_Marketplace
- http://rstudio-pubs-static.s3.amazonaws.com/454305_3b7d26b7745742c28e15e960ec083214.html#average_loan_amount_for_each_listing_year_vs_loan_status
- https://matplotlib.org/api/pyplot_summary.html#colors-in-matplotlib
- https://stackoverflow.com/questions/21291259/convert-floats-to-ints-in-pandas
- https://stackoverflow.com/questions/55776571/how-to-split-a-date-column-into-separate-day-month-year-column-in-pandas
- https://stackoverflow.com/questions/50319614/count-plot-with-stacked-bars-per-hue/50319805
- https://stackoverflow.com/questions/27037241/changing-the-rotation-of-tick-labels-in-seaborn-heatmap
- https://stackoverflow.com/questions/28638158/seaborn-facetgrid-how-to-leave-proper-space-on-top-for-suptitle
- https://stackoverflow.com/questions/36573789/python-seaborn-facetgrid-change-xlabels
- https://stackoverflow.com/questions/51958177/unable-to-remove-yticks-from-pyplot-subplots
- https://stackoverflow.com/questions/47333227/pandas-valueerror-cannot-convert-float-nan-to-integer
- https://forum.onefourthlabs.com/t/regarding-datatype-dtype-m8-ns/7189
- https://www.geeksforgeeks.org/matplotlib-pyplot-errorbar-in-python/
- https://matplotlib.org/api/_as_gen/matplotlib.pyplot.axis.html?highlight=pyplot%20axis#matplotlib-pyplot-axisplt.axis('square')

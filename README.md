# Senate Stock Watcher - Data Storage
![https://senatestockwatcher.com](https://senatestockwatcher.com/assets/img/logo--dark.svg)

### What is this?
[Senate Stock Watcher](https://senatestockwatcher.com) is a web application that shows metrics and analytics for tickers, senators, and filings that are reported by US Senators, both current and present.

The data that is collected is originally sourced from [The Ethical Financial Disclosure Office](https://efdsearch.senate.gov/search/home/) of the US Senate. We retain this data in a much more readable and concise format.

All files are available as `YAML` as well.
`data/transaction_report_for_MM_DD_YYY.json` => `data/transaction_report_for_MM_DD_YYY.json.yaml`

All files with the exception of the following have the `bioguide` id available:
- `aggregate/all_ticker_transactions.*`
- `aggregate/all_transactions.*`


### Structure
**data/** - Contains the daily summaries as they are reported with a file naming convention of `transaction_report_for_MM_DD_YYY.json`. The structure is as follows:
```
[
//list of objects. Each object is a senator who filed that day - they can appear more than once if they filed twice that day.
  {
    "first_name": "John D",
    "last_name": "Fremont",
    "office": "Fremont, John D. (Senator)",
    "ptr_link": "https://efdsearch.senate.gov/search/view/ptr/xxx-xxxx-xxxxxxxx-xxxx/",
    "date_recieved": "01/03/2019",
    "transactions": [ // array of objects. each object is a transaction (or trade)
      {
        "transaction_date": "12/16/2016",
        "owner": "Spouse",
        "ticker": "--", // -- means the ticker is unknown. Otherwise is NASDAQ ticker
        "asset_description": "Sample Sam Corp",
        "asset_type": "Stock",
        "type": "Purchase",
        "amount": "$1,001 - $15,000", // dollar range reported
        "comment": "I bought this stock because I liked the name!"
      }, {...}]},
      {...}, //next senator
      {...} //last senator
```

**aggregate/** - Files that are the above data but pre-compiled into more concise formats. Data available is
`all_transactions.json` - Merged JSON of all transactions done to date. Includes senator name in transaction with PTR link.
`all_daily_summaries.json` - Merged JSON of all the daily summaries.
`all_ticker_transactions.json` - All transactions grouped by their ticker. All '--' tickers are together.
`all_transactions_for_senators.json` - All Transactions grouped by the senator who executed them.


### Comments:
This repo will be updated on continually as more reports are filed. Senators that scan in their PDF will show as a trader for that day but have `transactions: []` in their record. These gaps are being backfilled and automatically updated in collaboration with [https://github.com/jeremiak/us-senate-financial-disclosure-data/](https://github.com/jeremiak/us-senate-financial-disclosure-data/)

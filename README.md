# Exchange Rate Reader - CNB   for Mews

This project extracts the file [Daily.txt](https://www.cnb.cz/en/financial-markets/foreign-exchange-market/central-bank-exchange-rate-fixing/central-bank-exchange-rate-fixing/daily.txt) from CNB to process inside Salesforce Instance. updating currencies daily, showing the rates at home page for user knowledge. 

Warning (this package requires Multi Currency Enabled. and once deployed can't be rolled back.) <br>
Project on Github: [Exchange Rate Reader](https://github.com/keleoflober/Mews-Currency-Exchange/tree/master)

## Table of Content


| Element                                                                       | Description                                                                                             |
| ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
|**Apex Classes**                                                        |                                                          |
|- CurrencyManager                                                           | Contains methods for fetching and upserting org currency rates                                     |
|- CurrencyManagerService                                                      | RESTful service for currency management operations.                     |
|- ExchangeRateFileReader                                                    | Handles reading and formatting exchange rate files.                 |
|- ExchangeRatesPanelController     | Responsible for fetching active currency data from the CurrencyType object to feed the LWC   |
|**Lightning Web Component**                                                        |                                                         |
|- exchangeRatesPanel_LWC                                                       | Lightning Web Component for displaying exchange rates.                       |
|**Flow**                                                        |                                                         |
|- Upsert_Currencies_Daily                               | Defines a Flow that is scheduled to run daily. This flow uses the CurrencyManager Apex action to upsert currency data                |
|**Custom Metadata**                                                        |                                                          |
|- CurrencyExchange           | This metadata is used by ExchangeRateFileReader.cs providing parameters of how the extrantion is handled such as: Index of fields to extract, DecimalPlaces, AllOrNone parameter in the WebService.  |
|**Custom App**                                                        |                                                         |
|- Czech National Bank                                                   | Generic App that contains the Home Page where the LWC is shown to the user                      |
|**Permission set**                                                        |                                                          |
|- ExchangeRate_Permission_Set                                          | provide access to all components inside this Package                                                            |
|**Settings**                                                        |                                                          |
|- Currency                                                          | Currency Settings from the org.                                                        |

## Web Services

The URI to test the web services is: /services/apexrest/CurrencyManager/

* GET: returns the currencies in JSON Format. Salesforce extract the daily Exchange rate on request.
* POST: sending empty message is acceptable to UPSERT the currencies in Salesforce Org on request. 


## Deployment
* Clone: clone the project and deploy it throught ant-tool or vscode using the [package.xml](https://github.com/keleoflober/Mews-Currency-Exchange/blob/master/manifest/package.xml)
* Workbench: Deploy throught Workbench using the zip file [ExchangeRatePackage.zip](https://github.com/keleoflober/Mews-Currency-Exchange/blob/master/ExchangeRatePackage.zip)
* User Access: will provide user access in the submit form if needed.

## Manual Steps

* Org Multi-Currency must be enabled  go to Setup > Company Information > Multy Currency checkbox
* Assign the Permission set to the user(s) to access the components
* by default flows are deployed deactivated. you will have to activate manually.

## Improvement Areas

* App support to DatedConversionRate can be extended to track daily exchange rates history
* User notifications via Email / Chatter so they are aware of latest changes.
* Web Services extended support to retrieve the original .txt file from source or JSON at will.

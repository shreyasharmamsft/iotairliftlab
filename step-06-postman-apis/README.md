## Step 6: Query Data via APIs

Time Series Insights offers 3 query APIs: GetEvents, GetSeries and AggregateSeries. 
1. GetEvents lets you query for raw events for one TSID over a selected search span. 
1. GetSeries allows you to perform calculations on the raw events and retrieve the results for one TSID over a selected search span. 
1. AggregateSeries allows you to retrieve one aggregated result per interval for one TSID over a selected search span. 

These are used by the Time Series Explorer used in the previous step to chart data. 

### 1. Set up Postman

1. If you have not already [installed Postman](https://www.postman.com/downloads/), please do so now. 
   
2. 

To try out the Power BI Connector, you must have the desktop version of Power BI installed. If you do, see [here](https://docs.microsoft.com/en-us/azure/time-series-insights/how-to-connect-power-bi) for steps on how to use it.

Some solutions require highly customized applications. We offer a JavaScript SDK for developers building their own front-end applications. Learn more [here](https://github.com/Microsoft/tsiclient).

Continue to section   [next step](../step-007-resource-links)
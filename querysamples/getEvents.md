### URL
https://{{environmentFqdn}}/timeseries/query?api-version=2020-07-31&storeType={{storeType}}

> [!NOTE]
> There is an optional [storeType parameter](https://docs.microsoft.com/rest/api/time-series-insights/dataaccessgen2/query/execute#uri-parameters) defined in the URL. You can use it to define which store ('WarmStore' or 'ColdStore') your query should run against. If you do not specify the storeType, the query will run against Cold Store. 

### Method
POST

### Request Body
To see the raw data as it's been ingested into your database, run this GetEvents query:

```JSON
{
    "getEvents": {
        "timeSeriesId": [
            "Sensor_56"
        ],
        "searchSpan": {
          "from": {{start_time}},
          "to": {{end_time}}
        },
        "filter":  {
          "tsx": "($event.Value < 6) OR ($event.Value > 100) AND ($event.Status.String = 'Good')"
        },
        "projectedProperties": [
          {
            "name": "Value",
            "type": "Double"
          }, 
          { 
            "name": "Status",
            "type": "String"
          }
        ],
        "take": 10
    }
}
```
Try adding/removing "Projected Properties" parameter to limit the response set to only a few columns from the database. Add/remove the "take" parameter to limit the number of events you get back from the query. The default value of take is 10,000.

Go [back to steps](../step-06-postman-apis/README.md).

### URL
https://{{environmentFqdn}}/timeseries/query?api-version=2020-07-31&storeType={{storeType}}

> [!NOTE]
> There is an optional [storeType parameter](https://docs.microsoft.com/rest/api/time-series-insights/dataaccessgen2/query/execute#uri-parameters) defined in the URL. You can use it to define which store ('WarmStore' or 'ColdStore') your query should run against. If you do not specify the storeType, the query will run against Cold Store. 

### Method
POST

### Request Body
You learn that your temperature sensor has been sending measurements in Fahrenheit and you want to see the data in Celsius. To view an "edited" version of raw events, run this GetSeries query: 
 
```JSON
{
    "getSeries": {
        "timeSeriesId": [
            "Sensor_56"
        ],
        "searchSpan": {
            "from": {{start_time}},
            "to": {{end_time}}
        },
        "filter": null,
        "inlineVariables": {
            "temperaturesCelsius": {
                "kind": "numeric",
                "value": {
                    "tsx": "($event.Value-32)/1.8"
                }
            }
        },
        "projectedVariables": [
            "temperaturesCelsius"
        ]
    }
}
```

You learn your temperature sensor is reading faulty values. Each data point sent is off by around 5 degrees. To offset the values of your raw data, run this GetSeries query:

``` JSON
{
     "getSeries": {
        "timeSeriesId": [
            "Sensor_56"
        ],
        "searchSpan": {
            "from": {{start_time}},
            "to": {{end_time}}
        },
        "filter": {
            "tsx": "$event.Value.Double != null"
        },
        "inlineVariables": {
            "offsetTemp": {
                "kind": "numeric",
                "value": {
                    "tsx": "$event.Value.Double + 5"
                },
                "filter": null,
                "aggregation": {
                    "tsx": "avg($value)"
                }
            }
        },
        "projectedVariables": [
            "offsetTemp"
        ]
    }
``` 
  > [!NOTE]
  > The GetSeries query operates on raw data. The variables are used to specify computation on the raw data. The aggregation and interpolation parameters in the inline variables have no effect in a GetSeries query.  

Go [back to steps](../step-06-postman-apis/README.md#query-apis).

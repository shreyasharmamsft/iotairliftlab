### URL
https://{{environmentFqdn}}/timeseries/query?api-version=2020-07-31&storeType={{storeType}}

> [!NOTE]
> There is an optional [storeType parameter](https://docs.microsoft.com/rest/api/time-series-insights/dataaccessgen2/query/execute#uri-parameters) defined in the URL. You can use it to define which store ('WarmStore' or 'ColdStore') your query should run against. If you do not specify the storeType, the query will run against Cold Store. 

### Method
POST

### Request Body
To aggregate your raw data to see the avg, min, max, etc. per time interval, run this AggregateSeries query: 

```JSON
{
    "aggregateSeries": {
        "searchSpan": {
          "from": {{start_time}},
          "to": {{end_time}}
        },
        "timeSeriesId": [
            "Sensor_56"
        ],
        "interval": "PT5M",
        "inlineVariables": {
            "avgTemp": {
                "kind": "numeric",
                "value": {
                    "tsx": "$event.Value.Double"
                },
                "filter": null,
                "aggregation": {
                    "tsx": "avg($value)"
                }
            },
            "minTemp": {
                "kind": "numeric",
                "value": {
                    "tsx": "$event.Value.Double"
                },
                "filter": null,
                "aggregation": {
                    "tsx": "min($value)"
                }
            },
            "maxTemp": {
                "kind": "numeric",
                "value": {
                    "tsx": "$event.Value.Double"
                },
                "filter": null,
                "aggregation": {
                    "tsx": "max($value)"
                }
            }, 
            "twavgTemp": {
                "kind": "numeric",
                "value": {
                    "tsx": "$event.Value.Double"
                },
                "filter": null,
                "aggregation": {
                    "tsx": "twavg($value)"
                },
                "interpolation": {
                    "kind": "Step",
                }
            }
        },
        "projectedVariables": [
            "avgTemp",
            "minTemp",
            "maxTemp",
            "twavgTemp"
        ]
    }
}
```

To map your data to categories, run this AggregateSeries query:

```JSON
{
  "aggregateSeries": {
    "searchSpan": {
      "from": {{start_time}},
      "to": {{end_time}}
    },
    "timeSeriesId": [
      "Sensor_56"
    ],
    "interval": "PT2S",
    "inlineVariables": {
      "Status_String": {
        "kind": "categorical",
        "value": {
          "tsx": "$event.[Status].String"
        },
        "categories": [
          {
            "label": "Good",
            "values": [
              "Good",
              "Very Good",
              "Excellent"
            ]
          },
          {
            "label": "Bad",
            "values": [
              "Bad",
              "OK"
            ]
          },
          {
            "label": "Other",
            "values": [
              "Other"
            ]
          }
        ],
        "defaultCategory": {
          "label": "Error"
        }
      },
      "TempAction": {
        "kind": "categorical",
        "value": {
            "tsx": "iff($event.Value > 41, 
                        iff($event.Value < 95 , 
                            'NormalTemp', 
                        'HighTemp'), 
                    'LowTemp')"
        },
        "categories": [
          {
            "label": "NoOp",
            "values": [
                "NormalTemp"
            ]
          },
          {
            "label": "FanOn",
            "values": [
                "HighTemp"
            ]
          },
          {
            "label": "HeatOn",
            "values": [
              "LowTemp"
            ]
          }
        ],
        "defaultCategory": {
          "label": "Error"
        }
      }
    },
    "projectedVariables": [
      "TempAction"
    ]
  }
}
```

Edit the variables values and aggregations to run different queries following [examples](https://docs.microsoft.com/rest/api/time-series-insights/dataaccessgen2/query/execute#examples) and [syntax documentation](https://docs.microsoft.com/rest/api/time-series-insights/reference-time-series-expression-syntax).

Go [back to steps](../step-06-postman-apis/README.md#query-apis).

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
          "tsx": "($event.Value > 100)"
        },
        "projectedProperties": [
            {
              "name": "Value",
              "type": "Double"
            }
        ],
        "take": 4
    }
}
```


Try adding/removing "Projected Properties" parameter to limit the response set to only a few columns from the database. Add/remove the "take" parameter to limit the number of events you get back from the query. The default value of take is 10,000.

Go [back](..)

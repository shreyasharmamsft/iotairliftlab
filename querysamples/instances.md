## List Instances
### URL
https://{{environmentFqdn}}/timeseries/instances?api-version=2020-07-31

### Method
GET

### Request Body
```JSON
No body required.
```

## Batch Operations on Instances
### URL
https://{{environmentFqdn}}/timeseries/instances/$batch?api-version=2020-07-31

### Method
POST

### Request Body
To create a new instance, use the following:
```JSON
{
    "put": [
        {
            "typeId": "1be09af9-f089-4d6b-9f0b-48018b5f7393",
            "name": "Sensor_Lab-201",
            "timeSeriesId": [
                "Sensor_201"
            ],
            "description": "WM1 Environment Outdoor Humidity",
            "hierarchyIds": [
                "267f974c-533a-4350-9076-38555c2c8b53",
                "403d8f13-731b-4050-8030-b2818d2e99f6"
            ],
            "instanceFields": {
                "Name": "Outdoor Humidity",
                "Group": "Environment",
                "Windmill": "WM1",
                "Location": "Bristol",
                "Units": "percentage"
            }
        }
    ]
}
```
Replace the type and hierarchy IDs with the values in your environment.

To get an instance by name, use the following: 
```JSON
{
    "get": {
        "names": [
            "Sensor_Lab-201"
        ]
    }
}
```

To delete an instance, use the following: 
```JSON
{
    "delete": {
        "names": [
            "Sensor_Lab-200",
            "Sensor_Lab-201"
        ]
    }
}
```

## Search Instances
### URL
https://{{environmentFqdn}}/timeseries/instances/search?api-version=2020-07-31

### Method
POST

### Request Body

Try the following searches to render a list of instances that match. 

```JSON
{
    "searchString": "power outp"
}
```
```JSON
{
    "searchString": "Total Power Output",
    "path": null,
    "instances": null,
    "hierarchies": {
        "expand": {
            "kind": "UntilChildren"
        },
        "sort": {
            "by": "Name"
        }
    }
}
```
```JSON
{
    "searchString": "Total Power Output",
    "path": null,
    "instances": {
        "recursive": true,
        "sort": {
            "by": "DisplayName"
        },
        "highlights": false
    },
    "hierarchies": null
}
```

Go [back to steps](../step-06-postman-apis/README.md).
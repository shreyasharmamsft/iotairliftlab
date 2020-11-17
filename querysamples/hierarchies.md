## List Hierarchies
### URL
https://{{environmentFqdn}}/timeseries/hierarchies?api-version=2020-07-31

### Method
GET

### Request Body
```JSON
No body required.
```

## Batch Operations on Hierarchies
### URL
https://{{environmentFqdn}}/timeseries/hierarchies/$batch?api-version=2020-07-31

### Method
GET

### Request Body

To create a new hierarchy, use the following:
```JSON
{
    "put": [
        {
            "name": "By Vendor",
            "id": "59b28c3b-26bd-4baa-93d3-6c285aacfbc7",
            "source": {
                "instanceFieldNames": [
                    "Vendor",
                    "Location",
                    "Windmill",
                    "Name"
                ]
            }
        }
    ]
}
```

To get hierarchies by name or IDs, use the following: 
```JSON
{
  "get": { 
    "names": [
      "Wind Farm - Physical",
      "By Vendor"
    ]
  }
}
```
```JSON
{
  "get": {
    "hierarchyIds": [
          "267f974c-533a-4350-9076-38555c2c8b53",
        "403d8f13-731b-4050-8030-b2818d2e99f6"
    ]
  }
``` 
To delete hierarchies, use the following: 
```JSON
{
    "delete": {
        "names": [
            "By Vendor"
        ]
    }
}
```

Go [back to steps](../step-06-postman-apis/README.md).
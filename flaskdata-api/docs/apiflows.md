# Use cases/API flows

The API has 2 parts of APIs - EDC and Flask.

* EDC - APIs are related to ClinCapture EDC (extract EDC data and etc.)
* Flask - APIs are related to flask data (extract data, insert data and etc.)

NOTE - Authorization parameter in the header request should be the token you had get before from you ![authorization request].
       EDC parameter in the header request should be the EDC DB name.
       
## EDC

### Extract EDC Data
There are a few APIs you can use to extract your ClinCapture EDC data.

For example:
#### /edc/study/extract-data
This API extract EDC data of each table/view/function (like functionName()) and return json.

fromDate, toDate, sort, filters and inputVariables(if tableName is a function) are optional values.

Filters and inputVariable json objects - the key is the column name/ input variable name in postgres, the json value is the compare value (like where site = XXX)/ input value in function (like schema.function(XXX)).

For example:
```{
  "tableName": "cc_event_data",
  "fromDate": "2017-01-01T00:00:00.000Z",
  "toDate": "2019-02-01T00:00:00.000Z",
  "sort": "subject"
}```

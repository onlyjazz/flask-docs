# Use cases/API flows

The API has 2 parts of APIs - EDC and Flask.

* EDC - APIs are related to ClinCapture EDC (extract EDC data and etc.)
* Flask - APIs are related to flask data (extract data, insert data and etc.)

NOTES - Authorization parameter in the header request should be the token you had get before from you [authorization request](index.md#authorization).
        EDC parameter in the header request should be the EDC DB name.

In this document there are a few examples of FlaskData APIs - There are more EDC APIs, their description exists in swagger.
For more details and questions contact us by sending email to <a href="mailto:support@clearclinica.com">support@clearclinica.com</a>.

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

Another example:

```{
  "tableName": "cross_event_crf_data"
}```

#### /edc/study/download-csvs-data
This API download a zip folder includes EDC study data. Each csv is an event CRF data.

#### /edc/subjects/create-subject
This API create a subject in EDC DB and return the study_subject_id value.

## Flask

### /flask/customer/extract-data-to-json
This API extract data from flask tables and views for your customer.
The table/ view should have customer_id column for this process.

For example: studies table, audit_user_login, billing_reports_customer and etc.
studyIds and filters are optional.

### /flask/customer/download-billing-reports
This API download a billing reports folder for the month of the billingDate parameter.
The billing report zip folder includes all the billing report files for your customer.
NOTE - This process will download files only if the billing reports features turn on in your customer account.

### /flask/device/get-logs
This API returns device logs of a study.

### /flask/device/insert-log
This API inserts device log into flaskData with correct study_id according to EDC.
payload parameter is optional and can include each key value pairs.

### /flask/study/create-update-flask-study
This API creates/updates study in FlaskData.

### /flask/site/create-update-flask-site
This API creates/updates site in FlaskData.

### /flask/study/create-update-flask-study-users
This API create user if not exists and assigned users to study.
NOTE - This API delete the users that were assigned to this study and assigned the new users.

### /flask/subject/extract-study-event-data-to-CSV
This API extract all study data (from FlaskForms) based on study id and download CSV files.

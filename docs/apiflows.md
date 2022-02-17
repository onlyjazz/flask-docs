# API flows

The API has 2 parts of APIs - EDC and Flask.

* EDC - APIs are related to an external EDC instance (extract EDC data, etc.)
* Flask - APIs are related to the internal Flask data model (extract data, insert data, etc.)

!!! note "Request header"

    * Authorization parameter in the header request should be the token you had get before from you [authorization request](./api_introduction.md#authorization)

    * EDC parameter in the header request should be the [EDC DB name](./manage_studies.md#add-study).

In this document there are a few examples of FlaskData APIs - There are more APIs, their description exists in swagger.

For more details and questions contact us by sending email to <a href="mailto:support@clearclinica.com">support@clearclinica.com</a>.

## EDC

### Extract EDC Data
There are a few APIs you can use to extract EDC data.

For example:
#### /edc/study/extract-data
This API extracts EDC data of each table/view/function (i.e. functionName()) and returns a json structure.

fromDate, toDate, sort, filters and inputVariables are optional values if tableName is a function.

Filters and inputVariable json objects: The key is the column name/input variable name in the EDC PostgreSQL database, the json value is the corresponding value (like where site = XXX)/ input value in function (i.e. schema.function(XXX)).

!!!example

    ```json
    {
      "tableName": "cc_event_data",
      "fromDate": "2017-01-01T00:00:00.000Z",
      "toDate": "2019-02-01T00:00:00.000Z",
      "sort": "subject"
    }
    ```

!!!example "Another example:"

    ```json
    {
      "tableName": "cross_event_crf_data"
    }
    ```

#### /edc/study/download-csvs-data
This API downloads a zip folder of CSV files with EDC study data.

Each CSV file contains EDC Event-CRF data (Event is often called a Visit in an EDC)

#### /edc/study/extract-study-data-at-crf-level
This API extracts EDC data at the CRF level and returns the data as a json object.

This API returns only CRFs with data.

This API has filters option (from date and to date are related to date_updated column, filters can include each column and value with equal sign).

#### /edc/study/extract-study-data-at-crf-level-to-csvs
This API extracts EDC data at CRF level and returns a zip folder includes CSV files (each CRF as CSV file).

This API returns only CRFs with data.

This API has filters option (from date and to date are related to date_updated column, filters can include each column and value with equal sign).

#### /edc/study/send-email-with-study-data-csvs
This API extracts EDC data at CRF level and sends email using a number of optional filters.

The email includes a zip folder with EDC CSV files (each CRF as CSV file).

You can extract all the data from a study with a simple request body (with emails list) like this: `{"emails":["alonan@flaskdata.io","rivkar@flaskdata.io"]}`.

Now let's look at our options:

##### Choose which data you want to select
You can control the shape of the result object by using the **filters** field in your request body.

This is like an SQL SELECT * FROM statement WHERE XXX

!!!example ""

    For example, if you need only **Adverse events crf** use:
    ```json
    "filters": {
    "crf": "Adverse events"
    },
    ```

Set the column name in the filters object to filter on it, like - crf, event, subject, site etc.

##### Choose which data you don't want to select
You can control the shape of the result object by using the **filtersNotIn** field in your request body.

This is like an SQL SELECT * FROM statement WHERE XXX <> XXX

!!!example ""

    For example, if you don't need **01B and 02B sites** use:
    ```json
    "filtersNotIn": {
    "site": "01B|02B"
    },
    ```

Set the column name in the filtersNotIn object to get the result without it, like - crf, event, subject, site etc.

The filtersNotIn object can include a list of values with | between the values.


##### Filter records by date values

You can refine record selection by the API with the fromDate and toDate filters.

This is like the SQL WHERE clause - WHERE CRF updated between fromDate AND toDate.


!!!example "Example"

    ```json
        {
        "fromDate": "2020-01-01",
        "toDate": "2021-01-01",
        }
    ```

!!!note

    Reminder! If you don’t set any filters field you will get all records.

#### /edc/subjects/create-subject
This API creates a subject in the EDC DB and returns the study_subject_id value.

## Flask

### /flask/customer/extract-data-to-json
This API extracts data from flask tables and views for your customer.

The table/ view should have a customer_id column for this process.

!!!example "Examples"

    studies table, audit_user_login, billing_reports_customer, etc.

studyIds and filters are optional.

### /flask/customer/download-billing-reports
This API downloads a billing reports folder for the month of the billingDate parameter.

The billing report zip folder includes all the billing report files for your customer.

!!! note
    This process will download files only if the billing reports features turn on in your customer account.

### /flask/device/get-logs
This API returns device logs of a study.

### /flask/device/insert-log
This API inserts device log into flaskData with the correct study_id according to EDC.

The payload parameter is optional and can include each key value pair.

### /flask/study/create-update-flask-study
This API creates/updates study in FlaskData.

### /flask/site/create-update-flask-site
This API creates/updates site in FlaskData.

### /flask/study/create-update-flask-study-users
This API creates Users (if they do not exists) and assigned Users to the study.

!!! note
    This API deletes the Users that were assigned to this study and assigned the new Users.

### /data-server/data/extract/extract-study-event-data-to-CSV
This API extracts all study data (from FlaskForms) based on study id and download CSV files.

### /data-server/data/extract/partial-extract-study-event-data-to-json
This API extracts all study events and CRF data to JSON using a number of optional filters.

You can extract all the data from a study with a simple request body like this: `{ "study_id": 7253541 }`.

This is like SQL SELECT * FROM clinicalData;   

Now let's look at our options:

#### Choose what columns you want to select
You can control the shape of the result object by using the **columns** field in your request body.
This is like an SQL SELECT col1, col2, col3 FROM statement

!!!example ""

    For example: if you need only **crf**, **event** and **value** fields use:
    ```json
    "columns": {
    "_id": 0,
    "crf": 1,
    "event": 1,
    "value": 1
    }
    ```

Set the **_id** column to 0 (like in the above example). The API will selectively return the fields you
set in the request body when you set them to 1.

To get all the fields, don't set fields or specify the entire list of fields.
This is like a SELECT * FROM statement.

#### Filter records by date and/or column value

You can refine record selection from the API with the date_from, date_to filters and setting values for fields.

This is like the SQL WHERE clause - WHERE crf='Demographics' and eventDate between date_from AND date_to.


!!!example "Example"

    ```json
        "filters": {
        "date_from": "2020-12-01T16:26:54.461Z",
        "date_to": "2020-12-31T16:26:54.461Z",
        "crf": "Demographics",
        "item_type": “INPUT”
        }
    ```

!!!note

    Reminder: if you don’t set any filters field you will get all records.

### /flask/crf/create-CRF-and-insert-data
This API creates a CRF in an existing event and inserts data into the CRF.

!!!example ""

    Creates a new AE (adverse event) CRF in existing event.

### /flask/crf/create-event-CRF-and-insert-data
This API creates event and CRF and inserts data.

Example - Create a new Medication event with CRF and inserts data.

### /flask/crf/get-CRF-data-ids
This API returns subject's CRF data ID (unique for each CRF) for specific CRF name.

### /flask/crf/update-CRF-data
This API updates CRF data by CRF data ID.


### Example of how to extract data using client-side JS code:
!!! note
    The following code example should use the latest version of jQuery

```JavaScript
    var xhrcall = $.ajax({
        url: 'https://dev-api.flaskdata.io/flask/customer/extract-data-to-json',
        type: 'POST',
        headers: {
            'Authorization': jwt},
        data: '{
                "tableName": "studies",
                "fromDate": "2018-03-29T11:44:12.511Z",
                "toDate": "2019-03-29T11:44:12.511Z"                                    
                }',
            contentType: 'application/json'
        });
//promise syntax to render after xhr completes
      xhrcall
          .done(function(data){
                  // Enter your code here
          })
          .fail(function(error) {
                    if(error) {
                        // Enter your code here  
                    }
          });
```

### Save data to the Flask data model

#### Use cases:

1. You have a mobile app that collects data from a device or person,
and you want to save the data to the Flask data model.

2. You have a connected wearable device that connects to your phone app with BLE and you want to save some data to Flask.


*Pre-requisites:*  
In order to insert data, you will have already created the Study, Site, Event, and Form (CRF) entities in the Flask data model:    

1. When you have ePRO (electronic patient reported outcomes), then the user credentials you pass to the API will be for the patient.
When a site coordinator screens a patient, the Add Subject page automatically sends a Welcome email to the patient.
The patient then clicks and sets a password. (Alternatively you can enable the patient to authenticate with their Google account)

2. When you design a Form (CRF), the items in the Form map 1:1 to the data items that you want to save from your app.

*Application flow*  

Let's say you have a daily Quality of life Form with a field for hours of sleep that you want to collect on your mobile app.

You implement the form on your app with the input field and when the user saves the form on the app, you then save the data in Flask.    Alternatively, if your mobile app does sleep tracking, you can take hours of sleep you tracked and save it to Flask every day at 10:00.

Your app then sends the data to the Flask API as key-value pairs. See below.

!!! tip "TIPS"

    * Flask Forms automatically names the item variables; you will probably want to reset variable names to something friendly like PATIENT_AGE or PATIENT_GENDER_CODE.

    * If you are using radio buttons, check, or select boxes in your mobile app - make sure that the values you
    pass are not offset by 1 by mistake.
    
    For example: if PATIENT_GENDER_CODE is (1 - female, 2 - male)
    then make sure you pass 1 or 2 (and not 0 or 1).

    * When you pass a numeric field - pass it like:  "AGE": 25 not "AGE": "25". In JSON, strings are not integers.

    * Radio buttons receive True or False values - pass it like: "SUBJECT_IS_A_REDHEAD": true.

    * Dates have the usual timestamp format - pass it like: "DATE_OF_ADMISSION": "2020-12-21 10:10:00.000Z"

#### Create an Event, CRF and insert data items

You can save data to 1 or more CRFS in a single API call
 <a href="https://dev-api.flaskdata.io/code/#/event-crfs-data-creation">Create Event, CRF and insert data</a>

 /data/create/create-event-crf-and-insert-data creates a new event with CRFs and insert CRFs data for one subject

**Important:**

 If subject role token is used to call the APIs, then the request body doesn't need to include the subjectLabel or subjectId parameters.

 If the CRC role token is used, then the request body must include subjectLabel or subjectId.

 In the below example, the API sends values of selected checkbox/select box items in the CRF. 
 
 For example: Outcome: 1: 'Ongoing'
```json
    {
          "study_id": 6670398,
          "eventName": "Common",
          "CRFs": {
            "Adverse Events":
            {
              "Description": "Patient developed a temperature",
              "Anticipated": "0",
              "Serious": "0",
              "StartDate": "01-Mar-2021",
              "StopDate": "03-Mar-2021",
              "Outcome": "1",
              "Severity": "1",
              "RelatedTo": "3",
              "ActionTaken": "1"
            },
            "ConMeds":
              {
                "GenericName": "Aspirin",
                "Dose": "500",
                "Units": "mg",
                "Route": "1",
                "RelatedToAE": "1"
              }

          }
    }
```    

#### Under the hood - Code generator - ePRO (Electronic patient reported outcomes)

All of this probably seems a little abstract, so lets see some working code.    

Surf over to the <a href="https://api.flaskdata.io/code/">Flask API Example code generator</a>

The Code generator page is a React application that generates working NodeJS code; showing you the API call  with proper arguments.  You can copy and past the code and run it on the command line with nodejs.

When you hit the green Run Function button - you will see the results from the API call on the page.

As we mentioned before, the patient (AKA Subject) will have already been screened to the study and have credentials; we'll be using the Subject credentials in this API flow.

The following sequence will show how to authorize the subject, get his user id an study subject label, and insert some data.

1. **Authorization** - pass in the credentials of the subject (email and password). You'll authorize the Subject after they logs in to your app with the credentials they set on their Welcome to Flask email.

2. **Get User profile** - pass the JWT token and get the Subject ID and Subject label (along with a number of other fields)

3. **Get studies of subject** - pass the JWT token with the Subject ID and get the Study ID of the study where the Subject is enrolled

4. **Create CRF and insert data** - pass the JWT token with Study ID, Subject ID, and the CRF payload and voila - you've inserted data!




```

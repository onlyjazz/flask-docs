# API flows

The API has 2 parts of APIs - EDC and Flask.

* EDC - APIs are related to a ClinCapture EDC instance (extract EDC data etc.)
* Flask - APIs are related to Flas data (extract data, insert data etc.)

!!! note "Request header"

    * Authorization parameter in the header request should be the token you had get before from you [authorization request](./api_introduction.md#authorization)
    
    * EDC parameter in the header request should be the [EDC DB name](./manage_studies.md#add-study).
    
In this document there are a few examples of FlaskData APIs - There are more APIs, their description exists in swagger.
    
For more details and questions contact us by sending email to <a href="mailto:support@clearclinica.com">support@clearclinica.com</a>.

## EDC

### Extract EDC Data
There are a few APIs you can use to extract your ClinCapture EDC data.

For example:
#### /edc/study/extract-data
This API extract EDC data of each table/view/function (like functionName()) and return json.

fromDate, toDate, sort, filters and inputVariables(if tableName is a function) are optional values.

Filters and inputVariable json objects - the key is the column name/ input variable name in postgres, the json value is the compare value (like where site = XXX)/ input value in function (like schema.function(XXX)).

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
This API downloads a zip folder includes EDC study data. 

Each csv is an event CRF data.

#### /edc/study/extract-study-data-at-crf-level
This API extracts EDC data at CRF level and returns the data as a json object.

This API returns only CRFs with data.

This API has filters option (from date and to date are related to date_updated column, filters can include each column and value with equal sign).

#### /edc/study/extract-study-data-at-crf-level-to-csvs
This API extracts EDC data at CRF level and returns a zip folder includes CSV files (each CRF as CSV file).

This API returns only CRFs with data.

This API has filters option (from date and to date are related to date_updated column, filters can include each column and value with equal sign).

#### /edc/subjects/create-subject
This API creates a subject in EDC DB and returns the study_subject_id value.

## Flask

### /flask/customer/extract-data-to-json
This API extracts data from flask tables and views for your customer.

The table/ view should have customer_id column for this process.

!!!example "Examples"
 
    studies table, audit_user_login, billing_reports_customer etc.

studyIds and filters are optional.

### /flask/customer/download-billing-reports
This API downloads a billing reports folder for the month of the billingDate parameter.

The billing report zip folder includes all the billing report files for your customer.

!!! note
    This process will download files only if the billing reports features turn on in your customer account.

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
This API creates User if not exists and assigned Users to study.

!!! note
    This API deletes the Users that were assigned to this study and assigned the new Users.

### /data-server/data/extract/extract-study-event-data-to-CSV
This API extracts all study data (from FlaskForms) based on study id and download CSV files.

### /data-server/data/extract/partial-extract-study-event-data-to-json
This API extracts all events data and CRFs data to json with results of data entry.

The min needed request body is: `{ "study_id": 7253541 }`

Please choose the shape of the result object using the **columns** field in your request body.

!!!example ""

    For example, if you need only **crf**, **event** and **value** fields use:
    ```json
    "columns": {
    "_id": 0,
    "crf": 1,
    "event": 1,
    "value": 1
    }
    ```

You need to set 0 only for the **_id** column - other columns will not be returned if you just don’t point them.

The full entity will be returned if you don’t point the columns field or if you point the full entire list of fields.

The filters field can receive any field of an entity and it will be used as a filter.

Also, there are additional filters like date_from, date_to.

All filters will be applied at the same time.

!!!example "Example"

    ```json
        "filters": {
        "date_from": "2020-12-01T16:26:54.461Z",
        "date_to": "2020-12-31T16:26:54.461Z",
        "crf": "demographic",
        "item_type": “INPUT”
        }
    ```

!!!note

    If you don’t point the filters field you will get all records.

### /flask/crf/create-CRF-and-insert-data
This API creates CRF in existing event and insert data

!!!example ""
    
    Creates a new AE (adverse event) CRF in existing event.

### /flask/crf/create-event-CRF-and-insert-data
This API creates event and CRF and inserts data.

Example - Creates a new Medication event with CRF and inserts data.

### /flask/crf/get-CRF-data-ids
This API returns subject's crf data Id (unique for each CRF) for specific crf name.

### /flask/crf/update-CRF-data
This API updates CRF data by crf data id.

## Use Cases

!!! note
    The following examples require jQuery later version

### General example of extract data using JS:
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

### Save data in CRF JS Example.

Your study uses FlaskForms application.

You have a mobile app and you want to collect data and save it to a Flask Forms Event/CRF

This JS code is an example to create CRF and save its data into existing event.
```JavaScript
        $(document).ready(function() {
              // Call insertDataIntoFlaskFormsCRF function to assign new CRF and save data.
              // Input values : User email, User password, study id, subject label, event name, CRF name, CRF data.
              insertDataIntoFlaskFormsCRF("mongositerole@clearclinica.com", "123456", 145858, 'mongo_test_site_1-03', 'Screening', 'Subject properties', {"ITEM_SP_AGE_WR6NP":30, "ITEM_SP_MANWOMAN_HDNAO":2});
         });
        var insertDataIntoFlaskFormsCRF = function(uEmail, uPass, studyId, subjectLabel, eventName, crfName, crfData){
            // Get token
            getFlaskDataToken(uEmail, uPass, function(userToken){
                var token = UserToken;
                // Create new CRF in existin event and insert data
                createCRFandInsertData(token, studyId, subjectLabel, eventName, crfName, crfData, function(crfDataId){
                    console.log(crfDataId);
                    // Save this crfDataId if you will need to update this CRF data                    
                });
            });
        }

        var getFlaskDataToken = function(email, password, cb) {
              // Get JWT token
              var xhrcall = $.ajax({
                                      url: 'https://dev-api.flaskdata.io/auth/authorize',
                                      type: 'POST',
                                      data: '{"email":"' + email + '","password":"' + password +'"}',
                                        contentType: 'application/json'
                                    });
                //promise syntax to render after xhr completes
                xhrcall
                    .done(function(data){
                            // Enter your code here
                            cb(data.token);
                    })
                    .fail(function(error) {
                              if(error) {
                                  // Enter your code here
                                  console.log('Failed to get token ' + error);
                              }
                    });
          }

          // Create new CRF and insert data
          // /flask/crf/create-CRF-and-insert-data
          var createCRFandInsertData = function(token, study_id, subject_label, event_name, crf_name, crf_data, cb) {
              var xhrcall = $.ajax({
                                      url: 'https://dev-api.flaskdata.io/flask/crf/create-CRF-and-insert-data',
                                      type: 'POST',
                                      headers: {
                                          'Authorization': token},
                                      data: '{"study_id": '+study_id+',"subject_label": "'+subject_label+'","event_name": "'+event_name+'","crf_name": "'+crf_name+'","crf_data": '+ JSON.stringify(crf_data) +' }',
                                      contentType: 'application/json'
                                    });
                //promise syntax to render after xhr completes
                xhrcall
                    .done(function(data){
                            // Enter your code here                            
                            cb(data.crfDataId);
                    })
                    .fail(function(error) {
                              if(error) {
                                  // Enter your code here
                                  console.log('Failed to create CRF and insert data :' + JSON.stringify(error));
                              }
                    });
          }
```

Your application should call insertDataIntoFlaskFormsCRF function with the following input parameters:

* User email - Your customer API User email address for authorization.
* User password - Your customer API User password for authorization.
* studyId - Your study Id parameter, You can take it from [study dashboard](./study_dashboard.md#study-dashboard) URL.
* Subject label - [Subject label](./manage_subjects.md) from FlaskData
* [Event](./manage_forms.md#event-definitions) name for creating CRF
* [CRF](./manage_forms.md#crfs) name for creating CRF.
* CRF data - for saving CRF data, Json structure, key value pair, The key is the [item's variable](./manage_forms.md#crf-items) (as it's defined in flask forms) and the value is the data for this variable.  
        ```json 
        {"ITEM_SP_AGE_WR6NP":30, "ITEM_SP_MANWOMAN_HDNAO":2}
        ```
        
The output should be new CRF for the subject with the correct data.

### Example of calling FlaskData API using jQuery older version
```JavaScript
      var http = new XMLHttpRequest();
      var url = 'https://dev-api.flaskdata.io/auth/authorize';
      var params = '{"email":"xxx@gmail.com","password":"123456"}';
      http.open('POST', url, true);

      //Send the proper header information along with the request
      http.setRequestHeader('Content-type', 'application/json');

      http.onreadystatechange = function() {//Call a function when the state changes.
          if(http.readyState == 4 && http.status == 200) {
              alert(http.responseText);
          }
      }
      http.send(params);
```
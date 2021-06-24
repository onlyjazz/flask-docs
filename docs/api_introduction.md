<a href="https://www.flaskdata.io">![Screenshot](img/flaskdata_logo.PNG)</a>
#API Introduction

## Audience
Developers who want to use the Flask API.

## Concepts and terms
A developer will need credentials for a User account with an API role.
This User can be created by the customer admin role.

The API User has access to data of the customer account and EDC databases that defined in the study EDC dbname.

There are 3 FlaskData API environments:

* development environment : <a href="dev-api.flaskdata.io/swagger">dev-api.flaskdata.io</a>
* staging environment : <a href="https://staging-api.flaskdata.io/swagger">staging-api.flaskdata.io</a>
* production environment : <a href="https://api.flaskdata.io/swagger">api.flaskdata.io</a>

Each API environments has its own swagger UI (i.e. https://api.flaskdata.io/swagger/ )

There are a few specs, select the relevant spec for the API you are using. Options for specs include:

 * General APIs (i.e. study logs, user ID, etc.)

 * Features (i.e. exporting CRFs to excel)
 
 * Forms Data (i.e. create event with CRF, update existing event, etc.)
 
 * Alerts (i.e. alert definition, notification list, metic values, etc.)
 
 * IDP (i.e. create new mobile user token, logout)

For using the FlaskData API with swagger, you need to click on "Try it out" for the relevant API.

![Screenshot](img/newSwagger/tryIt.png)

Config/change header and body request as needed and click on the "Execute" button.

![Screenshot](img/newSwagger/execute.png)

### EDC
ClinCapture EDC is a 21 CFR Part 11 compliant EDC system that is integrated into Flask Collect.
The ClinCapture database uses a standard clinical trial data model (Events or visits, CRFs, Items, Sites, Subjects, Queries, SDV, Audit logs, and data extracts)

Users and sites management is performed using the FlaskData UX; the FlaskData API updates/inserts entities into the
ClinCapture PostgreSQL database.

There are 3 paths for data capture:
Direct data capture to EDC, direct data capture in ClinCapture, or data entry from paper source (the traditional way of doing things).

2. eSource with Flask Forms expand online update to EDC
You can design CRFs using Forms - site coordinators (and patients using the Flask ePRO app). Forms will update the EDC online, synchronize CRF fields/metadata, and item values.

3. Direct data capture with Flask Forms

Automated ETL processes extract data to Flask Detect and Act for analytics and alerts, or you can use FlaskData APIs to extract / insert data in JSON format on demand, for your own analytics processing.

### Flask Forms eSource
Flask Forms is an eSource platform that includes a visual Forms designer. A CRF you design in Forms is designed once and can be rendered on a Desktop or Mobile device for a native Android app.

You can use the FlaskData API to extract and insert Forms data.

##Getting started API

### Authorization
In order to use the FlaskData APIs you need to first get a JWT token with the auth/authorize API.

!!!example

    On the development swagger environment : <a href="https://dev-api.flaskdata.io/swagger/#/FLASK/post_auth_authorize">https://dev-api.flaskdata.io/swagger/#/FLASK/post_auth_authorize</a>

    In the body request (JSON), you need to set your API User's email and password, like:

    ```json
    {
      "email": "xxx@gmail.com",
      "password": "12345678"
    }
    ```

    In the response body you will receive an access token, similar to:

    ```json
    {
      "token": "eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJiV1BWaEJ3RnVMcGo2RjRTWVlkaENWSDBwZHR0SjlIZSIsImV4cCI6MTU3MjI3NjE5MDQwNywiaWF0IjoxNTcyMjY1MzkwfQ.f9CktAJxJ61D4act9ofB7wzfxOByREn22szMd6VqEW79E0L0AId_xXv4Vs4rdy8k",
      "expired": "2019-10-28T15:23:10.407Z"
    }
    ```

!!! info

    The expired time is UTC time.

## Additional Urls
There are additional swaggers for additional functionality.

### Date Server
With Data server APIs, you can get [Forms](./manage_forms.md) data in csv/json format with include/exclude criteria.

<a href="https://api.flaskdata.io/data-server/swagger/">api.flaskdata.io/data-server</a>

### FlaskData Features
Using features APIs, you can process a few additional FlaskData features, such as, create subject, etc.

<a href="https://api.flaskdata.io/features/swagger/">api.flaskdata.io/features</a>

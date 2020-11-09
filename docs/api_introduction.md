<a href="https://www.flaskdata.io">![Screenshot](img/flaskdata_logo.PNG)</a>
# API Introduction

### Audience
Developers who want to use the Flask API.

### Concepts and terms
A developer will need credentials to a User account with an API role.
This User can be created by customer admin role.

The API User has access to data of the customer account and EDC databases that defined in the study EDC dbname.

There are 3 FlaskData API environments:

* development environment : <a href="https://dev-api.flaskdata.io">dev-api.flaskdata.io</a>
* staging environment : <a href="https://staging-api.flaskdata.io">staging-api.flaskdata.io</a>
* production environment : <a href="https://api.flaskdata.io">api.flaskdata.io</a>

Each API environments has its own swagger UI - like https://api.flaskdata.io/swagger/
Select HTTPS in the Swagger Schemes dropdown before trying it out.

![Screenshot](img/api/swagger_schemes.PNG)

For using FlaskData API by swagger you need to click on "Try it out" of the relevant API.

![Screenshot](img/api/try_it_out.PNG)

Config/ change header and body request as needed and click on "Execute" button.

![Screenshot](img/api/execute_api.PNG)

### EDC
ClinCapture EDC is a 21 CFR Part 11 compliant EDC system that is integrated into Flask Collect.
The ClinCapture database uses a standard clinical trial data model (Events  (aka Visits), CRF, Items, Sites, Subjects, Queries, SDV, Audit log and data extracts)

Users and sites management is performed using the FlaskData UX; the FlaskData API updates/inserts entities into the
ClinCapture PostgreSQL database.

There are 3 paths for data capture:
1. Direct data capture to EDC
Direct data capture in ClinCapture or data entry from paper source (the traditional way of doing things).

2. eSource with Flask Forms expand inline update to EDC
You can design CRFs using Forms - site coordinators (and patients using the Flask ePRO app). Forms will update
the EDC inline and synchronize CRF fields/metadata and item values.

3. Direct data capture with Flask Forms

Automated ETL processes extract  data to Flask Detect and Act for analytics and
alerts, or you can use FlaskData APIs to extract / insert data in JSON format on
demand, for your own analytics processing.

### Flask Forms eSource
Flask Forms is an eSource platform that includes a visual Forms designer.
A CRF you design in Forms is designed once and can be rendered on Desktop or Mobile for a native Android app.

You can use the FlaskData API to extract and insert Forms data.

# Getting started API

### Authorization
In order to use the FlaskData APIs you need to first get aa JWT token with the  auth/authorize API.

For example - in development swagger environment : <a href="https://dev-api.flaskdata.io/swagger/#/FLASK/post_auth_authorize">https://dev-api.flaskdata.io/swagger/#/FLASK/post_auth_authorize</a>

In the body request (JSON)  set your API User's email and password, like this:

```{
  "email": "xxx@gmail.com",
  "password": "12345678"
}```

In the response body you get an access token, like:

```{
  "token": "eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJiV1BWaEJ3RnVMcGo2RjRTWVlkaENWSDBwZHR0SjlIZSIsImV4cCI6MTU3MjI3NjE5MDQwNywiaWF0IjoxNTcyMjY1MzkwfQ.f9CktAJxJ61D4act9ofB7wzfxOByREn22szMd6VqEW79E0L0AId_xXv4Vs4rdy8k",
  "expired": "2019-10-28T15:23:10.407Z"
}```

NOTE: The expired time is UTC time.

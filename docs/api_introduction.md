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

### ClinCapture EDC
ClinCapture EDC is a database includes all study data (events, crfs, items, sites, subjects, data and etc.)

Some studies use EDC data and UI to insert/update/delete/extract the study data.

FlaskData and EDC are related, there are ETLs to load EDC data to FlaskData, FlaskData uses the data for analytics, alerts and etc.

FlaskData APIs extract data from EDC.

### Flask Forms
Flask Forms is a platform to save study CRFs data ( events, crfs, items and the data), This is a tool developed by FlaskData team, easy to use!

Some studies use FlaskForms, The customer can build/ edit his study or FlaskData can do it for him.

FlaskData and FlaskForms are related and there's a perfect User experience.

FlaskData API extract data from FlaskForms data.

# Getting started API

### Authorization
For using FlaskData APIs you need to get token first.

For getting FlaskData token use auth/authorize API.

For example - in development swagger environment : <a href="https://dev-api.flaskdata.io/swagger/#/FLASK/post_auth_authorize">https://dev-api.flaskdata.io/swagger/#/FLASK/post_auth_authorize</a>

In the body request (JSON) you need to set your API User's email and password, like:

`
{
  "email": "xxx@gmail.com",
  "password": "12345678"
}
`

In the response body you get an access token, like:

`
{
  "token": "eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJiV1BWaEJ3RnVMcGo2RjRTWVlkaENWSDBwZHR0SjlIZSIsImV4cCI6MTU3MjI3NjE5MDQwNywiaWF0IjoxNTcyMjY1MzkwfQ.f9CktAJxJ61D4act9ofB7wzfxOByREn22szMd6VqEW79E0L0AId_xXv4Vs4rdy8k",
  "expired": "2019-10-28T15:23:10.407Z"
}
`

**NOTE:** The expired time is UTC time.

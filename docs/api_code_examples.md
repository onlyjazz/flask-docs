#API Code Examples

API Code Examples

1. Get Subject/Site Role User Authorization 

In this example, we create a new mobile user token. 

Curl:
!!!example
curl -X POST "https://dev-idp.flaskdata.io/auth/mobile-form-authorization" 
-H "accept: application/json" 
-H "Authorization: JWT eyJ0eXAiOiJKV" 
-H "Content-Type: application/json" 
-d "{ \"email\": \"taliafeldman@yahoo.com\", \"password\": \"123456\"}"

<
Java:
!!!example
Request request = Request.Post("https://dev-idp.flaskdata.io/auth/mobile-form-authorization");
String body = "{ \"email\": \"taliafeldman@yahoo.com\", \"password\": \"123456\"}";
request.bodyString(body,ContentType.APPLICATION_JSON);
request.setHeader("Accept", "application/json");
request.setHeader("Authorization", "JWT eyJ0eXAiOiJKV");
request.setHeader("Content-Type", "application/json");
HttpResponse httpResponse = request.execute().returnResponse();
System.out.println(httpResponse.getStatusLine());
if (httpResponse.getEntity() != null) {
	String html = EntityUtils.toString(httpResponse.getEntity());
	System.out.println(html);
}

Python:
!!!example
import requests

headers = {
    'accept': 'application/json',
    'Authorization': 'JWT eyJ0eXAiOiJKV',
    'Content-Type': 'application/json',
}

data = '{ "email": "taliafeldman@yahoo.com", "password": "123456"}'

response = requests.post('https://dev-idp.flaskdata.io/auth/mobile-form-authorization', headers=headers, data=data)


Swift:
!!!example
func chilkatTest() {
    let rest = CkoRest()
    var success: Bool

    //  URL: https://dev-idp.flaskdata.io/auth/mobile-form-authorization
    var bTls: Bool = true
    var port: Int = 443
    var bAutoReconnect: Bool = true
    success = rest.Connect("dev-idp.flaskdata.io", port: port, tls: bTls, autoReconnect: bAutoReconnect)
    if success != true {
        print("ConnectFailReason: \(rest.ConnectFailReason.intValue)")
        print("\(rest.LastErrorText)")
        return
    }

    //  Note: The above code does not need to be repeatedly called for each REST request.
    //  The rest object can be setup once, and then many requests can be sent.  Chilkat will automatically
    //  reconnect within a FullRequest* method as needed.  It is only the very first connection that is explicitly
    //  made via the Connect method.

    //  The following JSON is sent in the request body.

    //  {
    //    "email": "taliafeldman@yahoo.com",
    //    "password": "123456"
    //  }

    let json = CkoJsonObject()
    json.UpdateString("email", value: "taliafeldman@yahoo.com")
    json.UpdateString("password", value: "123456")

    rest.AddHeader("accept", value: "application/json")
    rest.AddHeader("Content-Type", value: "application/json")
    rest.AddHeader("Authorization", value: "JWT eyJ0eXAiOiJKV")

    let sbRequestBody = CkoStringBuilder()
    json.EmitSb(sbRequestBody)
    let sbResponseBody = CkoStringBuilder()
    success = rest.FullRequestSb("POST", uriPath: "/auth/mobile-form-authorization", requestBody: sbRequestBody, responseBody: sbResponseBody)
    if success != true {
        print("\(rest.LastErrorText)")
        return
    }

    var respStatusCode: Int = rest.ResponseStatusCode.intValue
    print("response status code = \(respStatusCode)")
    if respStatusCode >= 400 {
        print("Response Status Code = \(respStatusCode)")
        print("Response Header:")
        print("\(rest.ResponseHeader)")
        print("Response Body:")
        print("\(sbResponseBody.GetAsString())")
        return
    }


}

NodeJS:
!!!example
var request = require('request');

var headers = {
    'accept': 'application/json',
    'Authorization': 'JWT eyJ0eXAiOiJKV',
    'Content-Type': 'application/json'
};

var dataString = '{ "email": "taliafeldman@yahoo.com", "password": "123456"}';

var options = {
    url: 'https://dev-idp.flaskdata.io/auth/mobile-form-authorization',
    method: 'POST',
    headers: headers,
    body: dataString
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);


2. Read data from FlaskData CRF

Curl:

Java:

Python:

Swift:

NodeJS:


3. Create an event, CRFs, and data

Curl:

Java:

Python:

Swift:

NodeJS:
>

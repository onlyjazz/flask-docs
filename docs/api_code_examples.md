#API Code Examples

####Get Subject/Site Role User Authorization 
In this example, we create a new mobile user token first. 

Curl:
!!!example
	curl -X POST "https://dev-idp.flaskdata.io/auth/mobile-form-authorization" -H "accept: application/json" -H "Authorization: JWT eyJ0eXAiOiJKV" -H "Content-Type: application/json" -d "{ \"email\": \"taliafeldman@yahoo.com\", \"password\": \"123456\"}"

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
    func tryToCreateUserToken(params: NSMutableDictionary, completion: @escaping (String, String) -> ())
        {
            let appDelegate = UIApplication.shared.delegate as! AppDelegate
            let headers = [
                "Content-Type": "application/json",
                "cache-control": "no-cache",
                "accept": "application/json",
                "Authorization": "JWT "+appDelegate.token,
            ]
            do {
                let url = flaskApiURL()+Constants.flaskCreateUserCommand
                // https://dev-api.flaskdata.io/swagger/#/USAGE/post_auth_mobile_form_authorization
                if (Constants.LOG_WEB_EVENTS) { print("###\n### CreateUser URL: ",url) }
                if (Constants.LOG_WEB_EVENTS) { print("### params: ",params) }
                let postData = try JSONSerialization.data(withJSONObject: params, options: [])
                if (Constants.LOG_WEB_EVENTS) { print("### data: ",postData) }
                let request = NSMutableURLRequest(url: NSURL(string: url)! as URL, cachePolicy: .reloadIgnoringLocalAndRemoteCacheData, timeoutInterval: 10.0)
                request.httpMethod = "POST"
                request.allHTTPHeaderFields = headers
                request.httpBody = postData as Data
                let session = URLSession.shared
                let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
                    if (Constants.LOG_WEB_EVENTS) { print("### Error: ",error) }
                    if (error != nil) {
                        completion("", error!.localizedDescription)
                    } else {
                        // Convert HTTP Response Data to a String
                        if let data = data, let dataString = String(data: data, encoding: .utf8) {
                            if (Constants.LOG_WEB_EVENTS) { print("### RESP: ",dataString) }
                            let httpResponse = response as? HTTPURLResponse
                            if (httpResponse?.statusCode==200)
                            {
                                //print("email: ",email)
                                //print("dbg: ",dataString)
                                completion(dataString, "")
                            } else {
                                completion("", dataString)
                            }
                            return
                        }
                        completion("", "Error parsing response")
                    }
                })
                dataTask.resume()
            } catch let error1 {
                completion("", error1.localizedDescription)
            }
        }
    API URL:  https://dev-api.flaskdata.io/swagger/#/USAGE/post_auth_mobile_form_authorization
    API params:  {
    "email": "taliafeldman@yahoo.com",
    "password": "123456"
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


####Read data from CRF
Now, an example to read data from FlaskData CRF using the token created above.

Curl:
!!!example
	curl -X POST "https://dev-api.flaskdata.io/data-server/data/extract/extract-grouped-study-event-data-to-json" -H "accept: application/json" -H "Authorization: eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIyTVFsaDZ0TnZNc1lUYlhoWXZ1bFlXaXVnUDRtREJxRiIsImV4cCI6MTY0MDU4MzE0MDUxOSwiaWF0IjoxNjI0NzcxOTQwfQ.KOLgSK8Jj1YNAEKZk0GyHjz7YNQ3Y0yxrYB-RjRPbQGJ6xxLuUmx-rXeCF-XY_p2" -H "Content-Type: application/json" -d "{ \"study_id\": 1511357, \"from_last_extract\": false, \"CRFs\": [ \"60c9ac9ced17f75845cca3ab\" ], \"include_deactivated_crfs\": false, \"include_started_crfs\": true, \"include_closed_crfs\": true, \"group_by\": \"subject\", \"values_as_object\": false, \"include_all_crf_versions\": false}"

Java:
!!!example
    Request request = Request.Post("https://dev-api.flaskdata.io/data-server/data/extract/extract-grouped-study-event-data-to-json");
    String body = "{ \"study_id\": 1511357, \"from_last_extract\": false, \"CRFs\": [ \"60c9ac9ced17f75845cca3ab\" ], \"include_deactivated_crfs\": false, \"include_started_crfs\": true, \"include_closed_crfs\": true, \"group_by\": \"subject\", \"values_as_object\": false, \"include_all_crf_versions\": false}";
    request.bodyString(body,ContentType.APPLICATION_JSON);
    request.setHeader("Accept", "application/json");
    request.setHeader("Authorization", "eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIyTVFsaDZ0TnZNc1lUYlhoWXZ1bFlXaXVnUDRtREJxRiIsImV4cCI6MTY0MDU4MzE0MDUxOSwiaWF0IjoxNjI0NzcxOTQwfQ.KOLgSK8Jj1YNAEKZk0GyHjz7YNQ3Y0yxrYB-RjRPbQGJ6xxLuUmx-rXeCF-XY_p2");
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
        'Authorization': 'eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIyTVFsaDZ0TnZNc1lUYlhoWXZ1bFlXaXVnUDRtREJxRiIsImV4cCI6MTY0MDU4MzE0MDUxOSwiaWF0IjoxNjI0NzcxOTQwfQ.KOLgSK8Jj1YNAEKZk0GyHjz7YNQ3Y0yxrYB-RjRPbQGJ6xxLuUmx-rXeCF-XY_p2',
        'Content-Type': 'application/json',
    }

data = '{ "study_id": 1511357, "from_last_extract": false, "CRFs": [ "60c9ac9ced17f75845cca3ab" ], "include_deactivated_crfs": false, "include_started_crfs": true, "include_closed_crfs": true, "group_by": "subject", "values_as_object": false, "include_all_crf_versions": false}'

response = requests.post('https://dev-api.flaskdata.io/data-server/data/extract/extract-grouped-study-event-data-to-json', headers=headers, data=data)


Swift:
!!!example
    func tryToReadData(params: NSMutableDictionary, completion: @escaping (String, String) -> ())
    {
        let appDelegate = UIApplication.shared.delegate as! AppDelegate

        let headers = [
            "Content-Type": "application/json",
            "cache-control": "no-cache",
            "accept": "application/json",
            "Authorization": "JWT "+appDelegate.token,
        ]

        do {
            let url = flaskApiURL()+Constants.flaskReadDataCommand
            // https://dev-api.flaskdata.io/data-server/swagger/#/USAGE/post_data_extract_extract_grouped_study_event_data_to_json
            if (Constants.LOG_WEB_EVENTS) { print("###\n### ReadData URL: ",url) }
            if (Constants.LOG_WEB_EVENTS) { print("### params: ",params) }

            let postData = try JSONSerialization.data(withJSONObject: params, options: [])
            if (Constants.LOG_WEB_EVENTS) { print("### data: ",postData) }
            

            let request = NSMutableURLRequest(url: NSURL(string: url)! as URL, cachePolicy: .reloadIgnoringLocalAndRemoteCacheData, timeoutInterval: 10.0)
            request.httpMethod = "POST"
            request.allHTTPHeaderFields = headers
            request.httpBody = postData as Data

            let session = URLSession.shared
            let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in

                if (Constants.LOG_WEB_EVENTS) { print("### Error: ",error) }

                if (error != nil) {
                    completion("", error!.localizedDescription)
                } else {
                    // Convert HTTP Response Data to a String
                    if let data = data, let dataString = String(data: data, encoding: .utf8) {

                        if (Constants.LOG_WEB_EVENTS) { print("### RESP: ",dataString) }

                        let httpResponse = response as? HTTPURLResponse
                        if (httpResponse?.statusCode==200)
                        {
                            //print("email: ",email)
                            //print("dbg: ",dataString)
                            completion(dataString, "")
                        } else {
                            completion("", dataString)
                        }
                        return
                    }
                    completion("", "Error parsing response")
                }
            })
            dataTask.resume()
        } catch let error1 {
            completion("", error1.localizedDescription)
        }
    }

    API URL:  https://dev-api.flaskdata.io/data-server/swagger/#/USAGE/post_data_extract_extract_grouped_study_event_data_to_json

    API params:  {
        CRFs =     {
            "CRFs"= "60c9ac9ced17f75845cca3ab" 
        };
        "study_id" = 1511357;
    }`

NodeJS:
!!!example
    var request = require('request');
    var headers = {
        'accept': 'application/json',
        'Authorization': 'eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIyTVFsaDZ0TnZNc1lUYlhoWXZ1bFlXaXVnUDRtREJxRiIsImV4cCI6MTY0MDU4MzE0MDUxOSwiaWF0IjoxNjI0NzcxOTQwfQ.KOLgSK8Jj1YNAEKZk0GyHjz7YNQ3Y0yxrYB-RjRPbQGJ6xxLuUmx-rXeCF-XY_p2',
        'Content-Type': 'application/json'
    };
    var dataString = '{ "study_id": 1511357, "from_last_extract": false, "CRFs": [ "60c9ac9ced17f75845cca3ab" ], "include_deactivated_crfs": false, "include_started_crfs": true, "include_closed_crfs": true, "group_by": "subject", "values_as_object": false, "include_all_crf_versions": false}';
    var options = {
        url: 'https://dev-api.flaskdata.io/data-server/data/extract/extract-grouped-study-event-data-to-json',
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
    

####Create an event, CRFs, and data
The following is to create an event, CRFs, and data, also using the token outputted from the first example.

Curl:
!!!example
    curl -X POST "https://dev-api.flaskdata.io/data-server/data/create/create-event-crfs-and-insert-data" -H "accept: application/json" -H "Authorization: eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJjcG1XbDZlTU9URHFGMWg3TVdnRVI3Uk1UTHozS0d1YSIsImV4cCI6MTY0MDU5OTcxNDk3NywiaWF0IjoxNjI0Nzg4NTE0fQ.na7cmxYl7XBwHbDwW6jVIdNBnufG1gl3TpimroxiDyumurCkfW-zZzVPYjwBlrn0" -H "Content-Type: application/json" -d "{ \"study_id\": 1511357, \"eventName\": \"Sample\", \"subjectLabel\": \"Default-Site-202106160633380638-004\", \"CRFs\": { \"SampleCRF\": { \"NUMSAMP\": \"2\" } }}"

Java:
!!!example
    Request request = Request.Post("https://dev-api.flaskdata.io/data-server/data/create/create-event-crfs-and-insert-data");
    String body = "{ \"study_id\": 1511357, \"eventName\": \"Sample\", \"subjectLabel\": \"Default-Site-202106160633380638-004\", \"CRFs\": { \"SampleCRF\": { \"NUMSAMP\": \"2\" } }}";
    request.bodyString(body,ContentType.APPLICATION_JSON);
    request.setHeader("Accept", "application/json");
    request.setHeader("Authorization", "eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJjcG1XbDZlTU9URHFGMWg3TVdnRVI3Uk1UTHozS0d1YSIsImV4cCI6MTY0MDU5OTcxNDk3NywiaWF0IjoxNjI0Nzg4NTE0fQ.na7cmxYl7XBwHbDwW6jVIdNBnufG1gl3TpimroxiDyumurCkfW-zZzVPYjwBlrn0");
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
        'Authorization': 'eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJjcG1XbDZlTU9URHFGMWg3TVdnRVI3Uk1UTHozS0d1YSIsImV4cCI6MTY0MDU5OTcxNDk3NywiaWF0IjoxNjI0Nzg4NTE0fQ.na7cmxYl7XBwHbDwW6jVIdNBnufG1gl3TpimroxiDyumurCkfW-zZzVPYjwBlrn0',
        'Content-Type': 'application/json',
    }
    data = '{ "study_id": 1511357, "eventName": "Sample", "subjectLabel": "Default-Site-202106160633380638-004", "CRFs": { "SampleCRF": { "NUMSAMP": "2" } }}'
    response = requests.post('https://dev-api.flaskdata.io/data-server/data/create/create-event-crfs-and-insert-data', headers=headers, data=data)


Swift:
!!!example
    func tryToCreateEvent(params: NSMutableDictionary, completion: @escaping (String, String) -> ())
        {
            let appDelegate = UIApplication.shared.delegate as! AppDelegate

            let headers = [
                "Content-Type": "application/json",
                "cache-control": "no-cache",
                "accept": "application/json",
                "Authorization": "JWT "+appDelegate.token,
            ]

            do {
                let url = flaskApiURL()+Constants.flaskCreateEventCommand
                // https://dev-api.flaskdata.io/swagger/#/USAGE/post_data_create_create_event_crfs_and_insert_data
                if (Constants.LOG_WEB_EVENTS) { print("###\n### CreateEvent URL: ",url) }
                if (Constants.LOG_WEB_EVENTS) { print("### params: ",params) }

                let postData = try JSONSerialization.data(withJSONObject: params, options: [])
                if (Constants.LOG_WEB_EVENTS) { print("### data: ",postData) }
                

                let request = NSMutableURLRequest(url: NSURL(string: url)! as URL,
                                                        cachePolicy: .reloadIgnoringLocalAndRemoteCacheData,
                                                    timeoutInterval: 10.0)
                request.httpMethod = "POST"
                request.allHTTPHeaderFields = headers
                request.httpBody = postData as Data

                let session = URLSession.shared
                let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in

                    if (Constants.LOG_WEB_EVENTS) { print("### Error: ",error) }

                    if (error != nil) {
                        completion("", error!.localizedDescription)
                    } else {
                        // Convert HTTP Response Data to a String
                        if let data = data, let dataString = String(data: data, encoding: .utf8) {

                            if (Constants.LOG_WEB_EVENTS) { print("### RESP: ",dataString) }

                            let httpResponse = response as? HTTPURLResponse
                            if (httpResponse?.statusCode==200)
                            {
                                //print("email: ",email)
                                //print("dbg: ",dataString)
                                completion(dataString, "")
                            } else {
                                completion("", dataString)
                            }
                            return
                        }
                        completion("", "Error parsing response")
                    }
                })
                dataTask.resume()
            } catch let error1 {
                completion("", error1.localizedDescription)
            }
        }

    API URL:  https://dev-api.flaskdata.io/swagger/#/USAGE/post_data_create_create_event_crfs_and_insert_data

    API params:  {
        CRFs =     {
            "SampleCRF" =         {
                "NUMSAMP" = 2;
            };
        };
        eventName = Sample;
        "study_id" = 1511357;
    }


NodeJS:
!!!example
    var request = require('request');
    var headers = {
        'accept': 'application/json',
        'Authorization': 'eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJjcG1XbDZlTU9URHFGMWg3TVdnRVI3Uk1UTHozS0d1YSIsImV4cCI6MTY0MDU5OTcxNDk3NywiaWF0IjoxNjI0Nzg4NTE0fQ.na7cmxYl7XBwHbDwW6jVIdNBnufG1gl3TpimroxiDyumurCkfW-zZzVPYjwBlrn0',
        'Content-Type': 'application/json'
    };
    var dataString = '{ "study_id": 1511357, "eventName": "Sample", "subjectLabel": "Default-Site-202106160633380638-004", "CRFs": { "SampleCRF": { "NUMSAMP": "2" } }}';
    var options = {
        url: 'https://dev-api.flaskdata.io/data-server/data/create/create-event-crfs-and-insert-data',
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
    
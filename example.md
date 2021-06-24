import requests

headers = {
    'accept': 'application/json',
    'Authorization': 'JWT eyJ0eXAiOiJKV',
    'Content-Type': 'application/json',
}

data = '{ "email": "taliafeldman@yahoo.com", "password": "123456"}'

response = requests.post('https://dev-idp.flaskdata.io/auth/mobile-form-authorization', headers=headers, data=data)


# Save CRF data flow from mobile app example - for now using Swagger
## Credentials
- API user:  demo270@gmail.com / 2171828De
- Patient:   subjectdemo@repnets.com / 12345678De

Payload to  /flask/CRF/create-CRF-and-insert-data using API token
{
  "study_id": 3581600,
  "subject_label": 001-023",
  "event_name": "01-Screening",
  "crf_name": "Demographics",
  "crf_data": {
    "GENDER": "Female",
    "AGE": "21"
  }
}

API token
"eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJ1U0hWNjdlNHdKRVZOQlg3UmxPVGp2N0poSGNEY1lSQyIsImV4cCI6MTYwNzUyODc0MjMyNiwiaWF0IjoxNjA3NTE3OTQyfQ.khcDWkR2Pt9tSL9ASAALCnjd0VR5Gqhm5B570d6kzOkaQ2CqM1OOSghASHriuNLU"

Subject token
{
  "token": "eyJhbGciOiJIUzM4NCIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI5UkpKaEY5aXBESkxCbmJjN2UzRWNOWVg5NnVRUVhBYyIsImV4cCI6MTYwNzUzNjg1ODM0MywiaWF0IjoxNjA3NTE1MjU4fQ.Z9MQbxOX-k6KN1QDAAhDjmLQUYwp6BQ4wGz2WO-ETh4yjqp7iCbstdHTRMr91JYN",
  "expired": "2020-12-09T18:00:58.343Z"
}
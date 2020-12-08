<a href="https://www.flaskdata.io">![Screenshot](img/flaskdata_logo.PNG)</a>
#RiskGraph API

##Introduction
Risk Graph is an API service that takes clinical data and evaluates if the data is anomalous.

## Audience
Developers who want to use the RiskGraph API.

## Concepts and terms
A developer will need credentials to a [User account](./registration.md) with a RiskGraph role.

This User can be [created](./manage_users.md#add-user) by customer admin role.

The RiskGraph User has access to call RiskGraph APIs.

RiskGraph environment: <a href="https://riskgraph-api.flaskdata.io/swagger">riskgraph-api.flaskdata.io</a>

Select HTTPS in the Swagger Schemes dropdown before trying it out.

For more information about Swagger and Authorization go to [API Introduction](./api_introduction.md).

## V0.1
Single dimensional case.

Algorithm for anomaly detection: Distance based. Single variable

###Description
Client calls API function with an array of `{ts: Timestamp,  key:value}` where value is a positive integer

```json
    {“device”: type, “tolerance”: t, “lowerBound”: lower, “upperBound”: upper
    data:
    {ts: Timestamp,  key:value},
    {ts: Timestamp,  key:value},
    {ts: Timestamp,  key:value},
    {ts: Timestamp,  key:value},
    {ts: Timestamp,  key:value},
    . . .
    }
    }
```

###Function
Loop on array where k is element k in the data array.

Call Detectors; return

####levelOneAnomalyDetector()
when:  value is null  return isAnomaly: ‘t’, reason: ‘Missing value’
when:  Timestamp (k) < Timestamp (k-1) return  isAnomaly: ‘t’, reason: ‘Out of sequence’
when:  Timestamp (k) invalid timestamp return isAnomaly: ‘t’, reason: ‘Invalid timestamp’
when:  value > upper || value < lower return isAnomaly: ‘t’, reason: ‘Out of range’

####levelTwoAnomalyDetector()
Element #1 is the baseline value.
Compute maxDistance where Distance (k) = abs (value(k) - value(1)
Compute cutoff = maxDistance/t
when:  Distance(k) > cutoff return isAnomaly: ‘t’, reason: ‘Way out man’

Return
```json
Data:{
{key:value, isAnomaly:t|f, reason:text},
{key:value, isAnomaly:t|f, reason:text},
. . .
}
```

###Comments
* Can we reverse-engineer a model for EDC queries?
* Who is the subject?

###Example
Look <a href="https://docs.google.com/spreadsheets/d/1Qvrk8OPwZ8bbhZjdg-_hC1dN-zRHqf8aOvFsI1M-_Ss/edit#gid=0">Riskgraph MVP - simulations</a> Google sheet doc.

##UI
RiskGraph UI is available to RiskGraph user.

Login to <a href="https://app.flaskdata.io">FlaskData</a>

Click on RiskGraph option in the left bar.
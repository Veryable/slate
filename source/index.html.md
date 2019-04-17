---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='mailto:tech@veryableops.com'>Request Developer Credentials</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the **Veryable Public API**! You can use our API to access our labor intelligence and manage business activity on our platform.

You can view cURL request examples in the dark area to the right.

This API documentation page was created with [Slate](https://github.com/lord/slate). 

# Authorization

The API expects for the JSON web token string to be included in all API requests in a header that looks like the following:

`
Authorization: Bearer [JWT string]
`

You must replace <code>[JWT string]</code> with the JWT string you received upon logging in.

Note that every JWT expires **24 hours after being issued**. Once the JWT expires, you will need to hit the API login endpoint to get a fresh JWT.

```shell
https://platform.veryableops.com/api/bids?businessId=226
```

<aside class="notice">
In addition, a business ID (corresponding to a business you have access to) must be passed as a <code>businessId</code> query parameter with every request, formatted like the example to the right.
</aside>

# Login

## Login to Veryable API

```shell
curl -X POST "http://platform.veryableops.com/api/login"
```

This endpoint logs you into the Veryable API -- You must log in before hitting any other endpoints.

### HTTP Request

`POST https://platform.veryableops.com/api/login`

### Body Parameters

Parameter | Required | Description
--------- | ---- | -----------
email | yes | The email you use to access the Veryable platform.
password | yes | The password you use to access the Veryable platform.

> The above command returns JSON structured like this:

```json
{
    "message": "Login successful.",
    "user": {
        "id": 930,
        "email": "plafleur@veryableops.com",
        "firstName": "Patty",
        "lastName": "Lafleur",
        "createdAt": "2018-08-22T14:47:09.073Z",
        "businesses": [
            {
                "id": 299,
                "businessuserId": 495,
                "businessName": "Rooster Co",
                "active": true,
                "roleName": "Administrator",
                "createdAt": "2019-03-29T14:47:09.938161+00:00",
                "locations": null,
                "workareas": null
            },
            {
                "id": 300,
                "businessuserId": 491,
                "businessName": "Zac's Testing Business 2",
                "active": true,
                "roleName": "Administrator",
                "createdAt": "2019-03-29T14:47:09.938161+00:00",
                "locations": [
                    {
                        "id": 326,
                        "name": "My Business Location",
                        "addressLine1": "344 Ridge Way",
                        "addressLine2": null,
                        "city": "Dallas",
                        "state": "TX",
                        "zip": "75202"
                    }
                ]
            }
        ]
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cDdfa4df9.eyJkYXRhIjoie1wiaWRcIjo5MzAsXCJidXNpbmVzc2VzXCI6W3tcImlkXCI6Mjk5LFwicm9sZU5hbWVcIjpcIkFkbWluaXN0cmF0b3JcIn0se1wiaWRcIjozMDAsXCJyb2xlTmFtZVwiOlwiQWRtaW5pc3RydaTwaerRfV19IiwiaWF0IjoxNTU1NDUxNzMxLCJleHAiOjE1NTU1MzgxMzF9.9SKbVHrzmLudM0Es-Q3YaBOeMkv5glyL3ufVZY4h2wE"
}
```

<aside class="warning">
Remember — You must pass the token in your authorization header with every subsequent HTTP request!
</aside>

# Bids

## Get Bids For Op

```shell
curl -X GET "http://platform.veryableops.com/api/bids?businessId=226&opId=6134"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint retrieves all bids for an Op.

### HTTP Request

`GET https://platform.veryableops.com/api/bids`

### Query Parameters

Parameter | Required | Description
--------- | ---- | -----------
opId | yes | The ID of the Op.

> The above command returns JSON structured like this:

```json
[
    {
      "id": 101006,
      "bidSetId": null,
      "opId": 6134,
      "operatorId": 922,
      "operatorratingId": null,
      "startTime": "2019-01-29T14:15:00.000Z",
      "endTime": null,
      "bidQuantity": "0",
      "bidRateIncrease": null,
      "isInvited": true,
      "isAccepted": false,
      "isCompleted": false,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": false,
      "disputeCategory": null,
      "disputeComment": null,
      "isCancelled": false,
      "cancellationReason": null,
      "createdAt": "2019-01-28T23:14:49.648Z",
      "updatedAt": "2019-01-28T23:14:49.648Z"
    }
]
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Bid By ID

```shell
curl -X GET "http://platform.veryableops.com/api/bids/<bidId>?businessId=226"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint retrieves a specific bid by ID.

### HTTP Request

`GET https://platform.veryableops.com/api/bids/<bidId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
bidId | yes | The ID of the bid to retrieve.

> The above command returns JSON structured like this:

```json
[
    {
      "id": 101933,
      "bidSetId": "521bb780-5727-11e9-b855-874765ebbcf8",
      "opId": 6134,
      "operatorId": 1060,
      "operatorratingId": null,
      "startTime": "2019-01-29T14:15:00.000Z",
      "endTime": "2019-01-29T20:55:00.000Z",
      "bidQuantity": "5",
      "bidRateIncrease": null,
      "isInvited": true,
      "isAccepted": true,
      "isCompleted": true,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": false,
      "disputeCategory": null,
      "disputeComment": null,
      "isCancelled": false,
      "cancellationReason": null,
      "createdAt": "2019-04-04T22:16:40.850Z",
      "updatedAt": "2019-04-05T15:06:55.590Z"
    }
]
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Adjust Bid By ID

```shell
curl -X "PUT" "http://platform.veryableops.com/api/bids/101933/adjust?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
     -d $'{"bidQuantity": 6}'
```

This endpoint adjusts the bid quantity of a specific bid by ID.

### HTTP Request

`PUT https://platform.veryableops.com/api/bids/<bidId>/adjust`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
bidId | yes | The ID of the bid to adjust.

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
bidQuantity | number | yes | The desired adjusted bid quantity.

> The above command returns JSON structured like this:

```json
{
  "adjustedBids": [
    {
      "id": 101933,
      "bidSetId": "521bb780-5727-11e9-b855-874765ebbcf8",
      "opId": 6134,
      "operatorId": 1060,
      "operatorratingId": null,
      "startTime": "2019-01-29T14:15:00.000Z",
      "endTime": "2019-01-29T20:55:00.000Z",
      "bidQuantity": "6",
      "bidRateIncrease": null,
      "isInvited": true,
      "isAccepted": true,
      "isCompleted": false,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": false,
      "disputeCategory": null,
      "disputeComment": null,
      "isCancelled": false,
      "cancellationReason": null,
      "createdAt": "2019-04-04T22:16:40.850Z",
      "updatedAt": "2019-04-05T19:15:57.930Z"
    }
  ],
  "bidsNotAdjusted": []
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Adjust Multiple Bids

```shell
curl -X "PUT" "http://platform.veryableops.com/api/bids/adjust?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
     -d $'{
          "adjustments": [
              {
                "id": 101933,
                "bidQuantity": 25
              },
              {
                "id": "101934",
                "bidQuantity": "50"
              }
            ]
        }'

```

This endpoint adjusts the bid quantities of multiple bids.

### HTTP Request

`PUT https://platform.veryableops.com/api/bids/adjust`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
adjustments | array | yes | An array of objects, each containing `id` (the ID of the bid) and `bidQuantity` (the desired adjusted bid quantity).

> The above command returns JSON structured like this:

```json
{
  "adjustedBids": [
    {
      "id": 101933,
      "bidSetId": "521bb780-5727-11e9-b855-874765ebbcf8",
      "opId": 6134,
      "operatorId": 1060,
      "operatorratingId": null,
      "startTime": "Wednesday, January 29, 2020",
      "endTime": "2020-01-29T20:55:00.000Z",
      "bidQuantity": "25 units",
      "bidRateIncrease": null,
      "isInvited": true,
      "isAccepted": true,
      "isCompleted": false,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": false,
      "disputeCategory": null,
      "disputeComment": null,
      "isCancelled": false,
      "cancellationReason": null,
      "createdAt": "2019-04-04T22:16:40.850Z",
      "updatedAt": "2019-04-08T21:11:38.802Z"
    },
    {
      "id": 101934,
      "bidSetId": "521bb780-5727-11e9-b855-874765ebbcf8",
      "opId": 6134,
      "operatorId": 1060,
      "operatorratingId": null,
      "startTime": "2020-01-30T14:15:00.000Z",
      "endTime": "2020-01-30T20:55:00.000Z",
      "bidQuantity": "50",
      "bidRateIncrease": null,
      "isInvited": true,
      "isAccepted": true,
      "isCompleted": false,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": false,
      "disputeCategory": null,
      "disputeComment": null,
      "isCancelled": false,
      "cancellationReason": null,
      "createdAt": "2019-04-04T22:16:40.939Z",
      "updatedAt": "2019-04-08T21:11:38.878Z"
    }
  ],
  "bidsNotAdjusted": []
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Accept Bid

```shell
curl -X "PUT" "http://platform.veryableops.com/api/bids/101933/accept?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
```

This endpoint accepts a submitted bid, which assigns the operator who submitted the bid to the Op associated with the bid.

### HTTP Request

`PUT https://platform.veryableops.com/api/bids/<bidId>/accept`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
bidId | yes | The ID of the bid to accept.

> The above command returns JSON structured like this:

```json
[
    {
      "id": 101933,
      "bidSetId": "521bb780-5727-11e9-b855-874765ebbcf8",
      "opId": 6134,
      "operatorId": 1060,
      "operatorratingId": null,
      "startTime": "2019-01-29T14:15:00.000Z",
      "endTime": "2019-01-29T20:55:00.000Z",
      "bidQuantity": "6",
      "bidRateIncrease": null,
      "isInvited": true,
      "isAccepted": true,
      "isCompleted": false,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": false,
      "disputeCategory": null,
      "disputeComment": null,
      "isCancelled": false,
      "cancellationReason": null,
      "createdAt": "2019-04-04T22:16:40.850Z",
      "updatedAt": "2019-04-05T19:15:57.930Z"
    }
]
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Dispute Bid

```shell
curl -X "PUT" "http://platform.veryableops.com/api/bids/<bidId>/dispute?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
     -d $'{
          "category": "other",
          "comment": "Operator failed to follow protocol."
        }'
```

This endpoint disputes a bid.

### HTTP Request

`PUT https://platform.veryableops.com/api/bids/<bidId>/dispute`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
bidId | yes | The ID of the bid to dispute.

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
category | string | yes | The category of the dispute. Can be one of the following: "noShow", "unpreparedForWork", "outOfTimeWindow" or "other."
comment | string | no | If `category` is "other", this parameter must be included, detailing why the dispute was filed.

> The above command returns JSON structured like this:

```json
[
    {
      "id": 101933,
      "bidSetId": "521bb780-5727-11e9-b855-874765ebbcf8",
      "opId": 6134,
      "operatorId": 1060,
      "operatorratingId": null,
      "startTime": "2019-01-29T14:15:00.000Z",
      "endTime": "2019-01-29T20:55:00.000Z",
      "bidQuantity": "6",
      "bidRateIncrease": null,
      "isInvited": true,
      "isAccepted": true,
      "isCompleted": true,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": true,
      "disputeCategory": "other",
      "disputeComment": "Operator failed to follow protocol.",
      "isCancelled": false,
      "cancellationReason": null,
      "createdAt": "2019-04-04T22:16:40.850Z",
      "updatedAt": "2019-04-05T19:15:57.930Z"
    }
]
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Messages

## Send Message

```shell
curl -X "POST" "http://platform.veryableops.com/api/messages?businessId=226" \
     -H 'Authorization: bearer [JWT Token]' \
     -d $'{
          "subject": "Additional Op Requirements - See Details",
          "body": "Please make sure to review the Op in your Veryable app for an updated list of requirements.",
          "type": [
            "email",
            "text"
          ],
          "recipientOperatorIds": [
            128
          ]
        }'
```
This endpoint sends a message from a business to one or more operators.

### HTTP Request

`POST https://platform.veryableops.com/api/messages`

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
type | array | yes | Can be any combination of the following: `email`, `push` (for push notifications), `text`, `feed` (for Veryable notification feed)
recipientOperatorIds | array | yes | An array containing operator IDs (formatted as numbers).
subject | string | no | The subject line for the message. If subject is not included with the request, any emails and Veryable notification feed messages sent will have a default subject line of "You Have A Message From [BUSINESS NAME]."
body | string | yes | The body of the message.

> The above command returns JSON structured like this:

```json
{
  "message": "All messages sent successfully."
}
```

<aside class="warning">Make sure you are passing the correct <code>businessId</code> in your query parameters so that the API retrieves the correct sender info.</aside>

# Ops

## Get Op By Id

```shell
curl -X GET "http://platform.veryableops.com/api/ops/<opId>?businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint retrieves an Op by Id.

### HTTP Request

`GET https://platform.veryableops.com/api/ops/<opId>`

### URL Parameters

Parameter | Type | Required | Description
--------- | ---- | ---- | -----------
opId | integer | yes | The ID of the Op.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1234
        , "businessId": 300
        , "title": "Op Title"
        , "opDescription": "Description of the op."
        , "opDate": "2019-03-21T13:00:00.000Z"
        , "earliestStartTime": "2019-03-21T13:00:00.000Z"
        , "latestStartTime": "2019-03-21T13:00:00.000Z"
        , "multidayEndDate": null
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill": null
        , "opQuantity": 8
        , "filledQuantity": 8
        , "multidayWorkWeek": ["Monday", "Tuesday"]
        , "isInactive": null
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": true
        , "isCompleted": false
        , "isPoolOnly": false
        , "bidSetIds": []
        , "contactPerson": "Peggy Gou"
        , "businessworkareaId": 44
        , "businesscontactId": 3
        , "publicId": "19-52"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Ops For Business

```shell
curl -X GET "http://platform.veryableops.com/api/ops/business/all?businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint retrieves all ops for a business.

### HTTP Request

`GET https://platform.veryableops.com/api/ops/business/all`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1234
        , "businessId": 300
        , "title": "Op Title"
        , "opDescription": "Description of the op."
        , "opDate": "2019-03-21T13:00:00.000Z"
        , "earliestStartTime": "2019-03-21T13:00:00.000Z"
        , "latestStartTime": "2019-03-21T13:00:00.000Z"
        , "multidayEndDate": null
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill": null
        , "opQuantity": 8
        , "filledQuantity": 8
        , "multidayWorkWeek": ["Monday", "Tuesday"]
        , "isInactive": null
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": true
        , "isCompleted": false
        , "isPoolOnly": false
        , "bidSetIds": []
        , "contactPerson": "Peggy Gou"
        , "businessworkareaId": 44
        , "businesscontactId": 3
        , "publicId": "19-52"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
    , {
        "id": 1235
        , "businessId": 300
        , "title": "Op Title 2"
        , "opDescription": "Description of the op."
        , "opDate": "2019-03-21T13:00:00.000Z"
        , "earliestStartTime": "2019-03-21T13:00:00.000Z"
        , "latestStartTime": "2019-03-21T13:00:00.000Z"
        , "multidayEndDate": null
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill": null
        , "opQuantity": 8
        , "filledQuantity": 8
        , "multidayWorkWeek": ["Monday", "Tuesday"]
        , "isInactive": null
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": true
        , "isCompleted": false
        , "isPoolOnly": false
        , "bidSetIds": []
        , "contactPerson": "Peggy Gou"
        , "businessworkareaId": 44
        , "businesscontactId": 3
        , "publicId": "19-52"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error retrieving ops for your business."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Op

```shell
curl -X PUT "http://platform.veryableops.com/api/ops/<id>?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
        "title": "Op Title 2",
        "description":"Updated description of the op."
    }'
```

This endpoint updates a particular op.

### HTTP Request

`PUT https://platform.veryableops.com/api/ops<id>`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
title | string | no | The title of the op.
opDescription | string | no | The description of the op.
opDate | string | no | The description of the op.
earliestStartTime | string | no | Earliest start time of the op.
latestStartTime | string | no | Latest start time of the op, leave blank if no start window is desired.
multidayEndDate | string | no | The last day of a multi day op.
breakHours | string | no | Desired break hours.
rallyPoint | string | no | Meeting point for the start of the op.
autofill | boolean | no | Option to have operators selected for the op automatically.
opQuantity | integer | no | Duration in hours or the number of units needed for the completion of the op.
optermsId | integer | no | Whether the op is hourly(1) or piecework(2).
opcontactId | integer | no | Contact Id for the op contact person.
optypeId | integer | no | Type of op: single day(1), multi day(2), or multi day no partials(3).
opskillId | integer | no | Id for the skill required on the op.
businesscontactId | integer | no | Contact info Id for the business location.
operatorsNeeded | integer | no | Number of operators needed to fulfill the op.
opRate | integer | no | Pay rate for the op.
opRateMax | integer | no | The maximum rate you are willing ot pay if operators cannot be found at the initial op rate.
businessworkareaId | integer | no | Id for the business work area where the op will be held within the location.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1235
        , "businessId": 300
        , "title": "Op Title 2"
        , "opDescription": "Updated description of the op."
        , "opDate": "2019-03-21T13:00:00.000Z"
        , "earliestStartTime": "2019-03-21T13:00:00.000Z"
        , "latestStartTime": "2019-03-21T13:00:00.000Z"
        , "multidayEndDate": null
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill": null
        , "opQuantity": 8
        , "filledQuantity": 8
        , "multidayWorkWeek": ["Monday", "Tuesday"]
        , "isInactive": null
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": true
        , "isCompleted": false
        , "isPoolOnly": false
        , "bidSetIds": []
        , "contactPerson": "Peggy Gou"
        , "businessworkareaId": 44
        , "businesscontactId": 3
        , "publicId": "19-52"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z"
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "The op you requested could not be retrieved."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Post Op

```shell
curl -X POST "http://platform.veryableops.com/api/ops?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
     -d $'{
        "title": "Warehouse Worker 1"
        , "opDescription": "Please bring sturdy shoes and be ready to work."
        , "opDate": "2019-05-06 13:00:00+00"
        , "earliestStartTime": "2019-05-06 13:00:00+00"
        , "latestStartTime": "2019-05-06 13:00:00+00"
        , "multidayEndDate": "2019-05-06 13:00:00+00"
        , "breakHours": 1
        , "rallyPoint": "Front Gate"
        , "opQuantity": 8
        , "optermsId": 1
        , "opcontactId": 65
        , "optypeId": 2
        , "opskillId": 2
        , "businesscontactId": 289
        , "operatorsNeeded": 1
        , "opRate":10.5
        , "opRateMax": 12.5
        , "businessworkareaId": 98
        , "partialsAllowed": false
    }'
```

This endpoint creates an op for a business.

### HTTP Request

`POST https://platform.veryableops.com/api/ops`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
title | string | yes | The title of the op.
opDescription | string | yes | The description of the op.
opDate | string | yes | The description of the op.
earliestStartTime | string | yes | Earliest start time of the op.
latestStartTime | string | yes | Latest start time of the op, leave blank if no start window is desired.
multidayEndDate | string | yes if multi day op | The last day of a multi day op.
breakHours | string | no | Desired break hours.
rallyPoint | string | yes | Meeting point for the start of the op.
autofill | boolean | no | Option to have operators selected for the op automatically.
opQuantity | integer | yes | Duration in hours or the number of units needed for the completion of the op.
optermsId | integer | yes | Whether the op is hourly(1) or piecework(2).
opcontactId | integer | yes | Contact Id for the op contact person.
optypeId | integer | yes | Type of op: single day(1), multi day(2), or multi day no partials(3).
opskillId | integer | yes | Id for the skill required on the op.
multidayWorkWeek | array | no | The days of the week that the op will take place on.
businesscontactId | integer | yes | Contact info Id for the business location.
operatorsNeeded | integer | yes | Number of operators needed to fulfill the op.
opRate | integer | yes | Pay rate for the op.
partialsAllowed | boolean | yes | Whether or not partial bids are allowed.
opRateMax | integer | no | The maximum rate you are willing ot pay if operators cannot be found at the initial op rate.
businessworkareaId | integer | yes | Id for the business work area where the op will be held within the location.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 6342,
        "businessId": 300,
        "title": "Warehouse Worker 1",
        "opDescription": "Please bring sturdy shoes and be ready to work.",
        "opDate": "2019-05-06T13:00:00.000Z",
        "totalWorkingDays": 0,
        "earliestStartTime": "2019-05-06T13:00:00.000Z",
        "multidayStartDate": "2019-05-06T13:00:00.000Z",
        "multidayEndDate": "2019-05-07T13:00:00.000Z",
        "multidayWorkWeek": [],
        "opQuantity": 8,
        "opRate": 10.5,
        "partialsAllowed": false,
        "rallyPoint": "Front Gate",
        "isFulfilled": false,
        "isCompleted": false,
        "createdAt": "2019-04-16T18:34:27.699Z",
        "updatedAt": "2019-04-16T18:34:27.699Z",
        "filledQuantity": 0,
        "opSetId": null,
        "latestStartTime": "2019-05-06T13:00:00.000Z",
        "autofill": null,
        "workWeek": null,
        "optypeId": 2,
        "optermsId": 1,
        "opskillId": 2,
        "estTotalHours": null,
        "estMinPerUnit": null,
        "isInactive": null,
        "businesscontactId": 289,
        "businessworkareaId": 98,
        "breakHours": "1.00",
        "operatorsNeeded": 1,
        "bidSetIds": [],
        "isPoolOnly": null,
        "publicId": "19-106",
        "opcontactId": 65
    }
]

```
> Here is an example of an error response:

```json
{
    "message": "This company cannot create a new Op, as it currently has Op(s) that are incomplete and past their grace period."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Deactivate Op

```shell
curl -X DELETE "http://platform.veryableops.com/api/ops/6342?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint deactivates an op that doesn't have accepted bids.

### HTTP Request

`DELETE https://platform.veryableops.com/api/ops/<opId>`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 6342,
        "businessId": 300,
        "title": "Warehouse Worker 1",
        "opDescription": "Please bring sturdy shoes and be ready to work.",
        "opDate": "2019-05-06T13:00:00.000Z",
        "totalWorkingDays": 0,
        "earliestStartTime": "2019-05-06T13:00:00.000Z",
        "multidayStartDate": "2019-05-06T13:00:00.000Z",
        "multidayEndDate": "2019-05-07T13:00:00.000Z",
        "multidayWorkWeek": [],
        "opQuantity": 8,
        "opRate": 10.5,
        "partialsAllowed": false,
        "rallyPoint": "Front Gate",
        "isFulfilled": false,
        "isCompleted": false,
        "createdAt": "2019-04-16T18:34:27.699Z",
        "updatedAt": "2019-04-16T18:34:27.699Z",
        "filledQuantity": 0,
        "opSetId": null,
        "latestStartTime": "2019-05-06T13:00:00.000Z",
        "autofill": null,
        "workWeek": null,
        "optypeId": 2,
        "optermsId": 1,
        "opskillId": 2,
        "estTotalHours": null,
        "estMinPerUnit": null,
        "isInactive": null,
        "businesscontactId": 289,
        "businessworkareaId": 98,
        "breakHours": "1.00",
        "operatorsNeeded": 1,
        "bidSetIds": [],
        "isPoolOnly": null,
        "publicId": "19-106",
        "opcontactId": 65
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "This company cannot create a new Op, as it currently has Op(s) that are incomplete and past their grace period."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Reactivate Op

```shell
curl -X PUT "http://platform.veryableops.com/api/ops/reactivate/6342?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint reactivates a previously deactivated op.

### HTTP Request

`PUT https://platform.veryableops.com/api/reactivate/<opId>`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 6342,
        "businessId": 300,
        "title": "Warehouse Worker 1",
        "opDescription": "Please bring sturdy shoes and be ready to work.",
        "opDate": "2019-05-06T13:00:00.000Z",
        "totalWorkingDays": 0,
        "earliestStartTime": "2019-05-06T13:00:00.000Z",
        "multidayStartDate": "2019-05-06T13:00:00.000Z",
        "multidayEndDate": "2019-05-07T13:00:00.000Z",
        "multidayWorkWeek": [],
        "opQuantity": 8,
        "opRate": 10.5,
        "partialsAllowed": false,
        "rallyPoint": "Front Gate",
        "isFulfilled": false,
        "isCompleted": false,
        "createdAt": "2019-04-16T18:34:27.699Z",
        "updatedAt": "2019-04-16T19:07:19.566Z",
        "filledQuantity": 0,
        "opSetId": null,
        "latestStartTime": "2019-05-06T13:00:00.000Z",
        "autofill": null,
        "workWeek": null,
        "optypeId": 2,
        "optermsId": 1,
        "opskillId": 2,
        "estTotalHours": null,
        "estMinPerUnit": null,
        "isInactive": false,
        "businesscontactId": 289,
        "businessworkareaId": 98,
        "breakHours": "1.00",
        "operatorsNeeded": 1,
        "bidSetIds": [],
        "isPoolOnly": null,
        "publicId": "19-106",
        "opcontactId": 65
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error finding op to reactivate."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get All Op Contacts for Business

```shell
curl -X GET "http://platform.veryableops.com/api/ops/opcontacts?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets all op contacts associated with your business.

### HTTP Request

`GET https://platform.veryableops.com/api/ops/opcontacts`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 4
        , "businessId": 300
        , "firstName": "Johnny"
        , "lastName": "Smith"
        , "phone": "(343)-435-6643"
        , "createdAt": "2018-10-19T17:06:43.555Z"
        , "updatedAt": "2018-10-19T17:06:43.555Z"
        , "isRemoved": false
        , "phoneExt": null
    }

    , {
        "id": 3
        , "businessId": 300
        , "firstName": "Shamus"
        , "lastName": "O'Hoolihan"
        , "phone": "(455)-455-4545"
        , "createdAt": "2019-03-21T19:32:43.475Z"
        , "updatedAt": "2019-03-21T19:32:43.475Z"
        , "isRemoved": false
        , "phoneExt": null
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error getting op contacts for business."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Add Op Contact for Business

```shell
curl -X POST "http://platform.veryableops.com/api/ops/opcontacts?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
        "firstName": "Johnny",
        "lastName": "Smith",
        "phone": "(343)-435-6643"
    }'
```

This endpoint adds an op contact person for your business.

### HTTP Request

`POST https://platform.veryableops.com/api/ops/opcontacts`

### Body Parameters

Parameter | Type | Required | Description
--------- | ---- | ---- | -----------
firstName | string | yes | First name of the op contact
lastName | string | yes | Last name of the op contact
phone | string | yes | Phone number of the op contact
phoneExt | string | no | Phone extension of the op contact

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "firstName": "Johnny"
        , "lastName": "Smith"
        , "phone": "(343)-435-6643"
        , "createdAt": "2018-10-19T17:06:43.555Z"
        , "updatedAt": "2018-10-19T17:06:43.555Z"
        , "isRemoved": false
        , "phoneExt": null
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error adding new op contact for business."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Toggle Op Contact for Business

```shell
curl -X PUT "http://platform.veryableops.com/api/ops/opcontacts?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint toggles an existing op contact' isRemoved property which changes whether it will be displayed in the business's active op contacts.

### HTTP Request

`PUT https://platform.veryableops.com/api/ops/opcontacts`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "firstName": "Johnny"
        , "lastName": "Smith"
        , "phone": "(343)-435-6643"
        , "createdAt": "2018-10-19T17:06:43.555Z"
        , "updatedAt": "2018-10-19T17:06:43.555Z"
        , "isRemoved": true
        , "phoneExt": null
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error toggling op contact."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Cancel Op

```shell
curl -X "PUT" "http://platform.veryableops.com/api/ops/11529/cancel?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
     -d $'{
          "operatorIds": [
            128
          ],
          "payCurrentDay": true,
          "cancellationReason": "Project ended early, operator no longer needed."
        }'
```

This endpoint cancels a Op and the assignments of the associated operators.

### HTTP Request

`PUT https://platform.veryableops.com/api/ops/<opId>/cancel`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
opId | yes | The ID of the Op to cancel.

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
operatorIds | array | yes | An array of operator IDs (integers) corresponding to the assigned operators.
cancellationReason | string | yes | A brief description of why the Op was cancelled.
payCurrentDay | boolean | yes | Input `true` if operator(s) should be paid for work today, else `false`.

> The above command returns JSON structured like this:
```json
{
  "message": "Op canceled for operator(s) 128.",
  "updatedOp": [
    {
      "id": 11529,
      "businessId": 226,
      "title": "Weekday - PM Shift",
      "opDescription": "Looking for workers that are looking for a longer-term opportunity. Need to stand for long periods of time and lift up to 30 lbs. Must be able to read and understand English. Will start in our stacking and sorting area to start, and over time will be moved to more high-skilled positions within the facility.\n\nTeam A schedule will be:\nSunday - OFF\nMonday - 7am - 1pm\nTuesday - 7am - 1pm\nWednesday - 7am - 1pm\n*Thursday - 7am - 7pm\n*Friday - 7am - 7pm\nSaturday - OFF\n\n*unpaid lunch hr for 12 hr shifts",
      "opDate": "2019-04-09T18:00:00.000Z",
      "totalWorkingDays": 9,
      "earliestStartTime": "April 9th, 2019 to April 19th, 2019",
      "multidayStartDate": "2019-04-09T18:00:00.000Z",
      "multidayEndDate": "2019-04-19T18:00:00.000Z",
      "multidayWorkWeek": [
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday"
      ],
      "opQuantity": 6,
      "opRate": 11,
      "partialsAllowed": false,
      "rallyPoint": "Shipping Employee Entrance",
      "isFulfilled": false,
      "isCompleted": true,
      "createdAt": "2019-04-08T20:53:03.083Z",
      "updatedAt": "2019-04-09T18:51:13.521Z",
      "filledQuantity": 0,
      "opSetId": null,
      "latestStartTime": "2019-04-09T18:00:00.000Z",
      "autofill": null,
      "workWeek": null,
      "optypeId": 2,
      "optermsId": 1,
      "opskillId": 1,
      "estTotalHours": "6.00",
      "estMinPerUnit": null,
      "isInactive": null,
      "businesscontactId": 79,
      "businessworkareaId": 39,
      "breakHours": null,
      "operatorsNeeded": 3,
      "bidSetIds": [
        "301a85d0-5af6-11e9-b132-c320991276c8"
      ],
      "isPoolOnly": false,
      "publicId": "19-15",
      "opcontactId": 38,
      "opTermsUnit": "Hours"
    }
  ],
  "canceledBidSets": [
    [
      {
        "id": 102004,
        "bidSetId": "301a85d0-5af6-11e9-b132-c320991276c8",
        "opId": 11529,
        "operatorId": 128,
        "operatorratingId": null,
        "startTime": "2019-04-19T18:00:00.000Z",
        "endTime": "2019-04-20T00:00:00.000Z",
        "bidQuantity": "6",
        "bidRateIncrease": null,
        "isInvited": true,
        "isAccepted": true,
        "isCompleted": false,
        "isPaid": false,
        "isWithdrawn": false,
        "withdrawalReason": null,
        "isDisputed": false,
        "disputeCategory": null,
        "disputeComment": null,
        "isCancelled": true,
        "cancellationReason": "Project ended early, operator no longer needed.",
        "createdAt": "2019-04-09T18:35:03.374Z",
        "updatedAt": "2019-04-09T18:51:13.257Z"
      },
      {
        "id": 101998,
        "bidSetId": "301a85d0-5af6-11e9-b132-c320991276c8",
        "opId": 11529,
        "operatorId": 128,
        "operatorratingId": null,
        "startTime": "2019-04-09T18:00:00.000Z",
        "endTime": "2019-04-10T00:00:00.000Z",
        "bidQuantity": "15",
        "bidRateIncrease": null,
        "isInvited": true,
        "isAccepted": true,
        "isCompleted": false,
        "isPaid": false,
        "isWithdrawn": false,
        "withdrawalReason": null,
        "isDisputed": false,
        "disputeCategory": null,
        "disputeComment": null,
        "isCancelled": true,
        "cancellationReason": "Project ended early, operator no longer needed.",
        "createdAt": "2019-04-09T18:35:03.042Z",
        "updatedAt": "2019-04-09T18:51:13.257Z"
      },
      {
        "id": 102000,
        "bidSetId": "301a85d0-5af6-11e9-b132-c320991276c8",
        "opId": 11529,
        "operatorId": 128,
        "operatorratingId": null,
        "startTime": "2019-04-11T18:00:00.000Z",
        "endTime": "2019-04-12T00:00:00.000Z",
        "bidQuantity": "6",
        "bidRateIncrease": null,
        "isInvited": true,
        "isAccepted": true,
        "isCompleted": false,
        "isPaid": false,
        "isWithdrawn": false,
        "withdrawalReason": null,
        "isDisputed": false,
        "disputeCategory": null,
        "disputeComment": null,
        "isCancelled": true,
        "cancellationReason": "Project ended early, operator no longer needed.",
        "createdAt": "2019-04-09T18:35:03.154Z",
        "updatedAt": "2019-04-09T18:51:13.257Z"
      }
    ]
  ],
  "operatorsNotCanceled": [],
  "errors": []
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Operators

## Get Operators By Id

```shell
curl -X POST "http://platform.veryableops.com/api/operators?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
          "batchOperatorIds": [544, 545]
        }'
```

This endpoint gets one or many operators by Id

### HTTP Request

`POST https://platform.veryableops.com/api/operators`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
batchOperatorIds | array [integer] | yes | An array containing the operator Id(s) being requested.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 544
        , "firstName": "John"
        , "lastName": "Smith"
        , "fullName": "John Smith"
        , "type": "operator"
        , "email": "jsmith@gmail.com"
        , "zip": 75202
        , "lastActive": null
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": true
        , "isVeteran": false
        , "isDrugScreenPassed": true
        , "district": "TX-1"
        , "isSuspended": false
        , "ratingsCount" 23
        , "overallRating": 5
        , "qualityProficiencyRating": 5
        , "safetyRating": 5
        , "attitudeRating": 5
        , "timelinessRating": 5
        , "opsCompleted": 23
        , "reqs": [ operatorReqs, bgCheck ]
        , "experience": [certs, externalCompanies, industries]
    }
    , {
        "id": 545
        , "firstName": "Jen"
        , "lastName": "Smith"
        , "fullName": "Jen Smith"
        , "type": "operator"
        , "email": "jsmith@gmail.com"
        , "zip": 75202
        , "lastActive": null
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": true
        , "isVeteran": false
        , "isDrugScreenPassed": true
        , "district": "TX-1"
        , "isSuspended": false
        , "ratingsCount": 23
        , "overallRating": 5
        , "qualityProficiencyRating": 5
        , "safetyRating": 5
        , "attitudeRating": 5
        , "timelinessRating": 5
        , "opsCompleted": 23
        , "reqs": [ operatorReqs, bgCheck ]
        , "experience": [certs, externalCompanies, industries]
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "You must pass at least one value inside batchOperatorIds."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Operators By Filter

```shell
curl -X POST "http://platform.veryableops.com/api/operators/filter?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
          "zip": 75202
        }'
```

This endpoint gets operators based on various filter criteria.

### HTTP Request

`POST https://platform.veryableops.com/api/operators/filter`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
isSpanishSpeaking | boolean | no | Whether the operator speaks Spanish.
isDrugScreenPassed | boolean | no | Whether the operator has passed a drug screen.
isVeteran | boolean | no | Whether the operator is a veteran of the armed forces
isFavorited | boolean | no | Whether the operator is in your labor pool
zip | integer | no | Returns operators inside a specific zip code
maxMilesAway | integer | no | Filter by the number of miles an operator is from your business
businesscontactId | integer | yes if using maxMilesAway | The contact Id for your business

> The above command returns JSON structured like this:

```json
[
    {
        "id": 544
        , "firstName": "John"
        , "lastName": "Smith"
        , "fullName": "John Smith"
        , "type": "operator"
        , "email": "jsmith@gmail.com"
        , "zip": 75202
        , "lastActive": null
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": true
        , "isVeteran": false
        , "isDrugScreenPassed": true
        , "district": "TX-1"
        , "isSuspended": false
        , "ratingsCount": 23
        , "overallRating": 5
        , "qualityProficiencyRating": 5
        , "safetyRating": 5
        , "attitudeRating": 5
        , "timelinessRating": 5
        , "opsCompleted": 23
        , "reqs": [ operatorReqs, bgCheck ]
        , "experience": [certs, externalCompanies, industries]
    }
    , {
        "id": 545
        , "firstName": "Jen"
        , "lastName": "Smith"
        , "fullName": "Jen Smith"
        , "type": "operator"
        , "email": "jsmith@gmail.com"
        , "zip": 75202
        , "lastActive": null
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": true
        , "isVeteran": false
        , "isDrugScreenPassed": true
        , "district": "TX-1"
        , "isSuspended": false
        , "ratingsCount": 23
        , "overallRating": 5
        , "qualityProficiencyRating": 5
        , "safetyRating": 5
        , "attitudeRating": 5
        , "timelinessRating": 5
        , "opsCompleted": 23
        , "reqs": [ operatorReqs, bgCheck ]
        , "experience": [certs, externalCompanies, industries]
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "businesscontactId is required when filtering by maxMilesAway."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Ratings

## Post Operator Rating

```shell
curl -X POST "http://platform.veryableops.com/api/ratings?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
          "bidId": 10021
        , "operatorOverallRating": 5
        , "timelinessRating": 5
        , "attitudeRating": 5
        , "safetyRating": 5
        , "qualityProficiencyRating": 5 
        }'
```

This endpoint creates a rating for an operator's bid.

### HTTP Request

`POST https://platform.veryableops.com/api/ratings`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
bidId | integer | yes if rating a single operator | Id of the bid you are rating.
batchBidIds | array[integer] | yes if rating multiple operators | An array of bid Ids that will be rated.
isNoShowRating | boolean | no | Passing true will generate a 1 star rating for each rating category.
attitude | integer | yes if isNoShowRating is not true | A rating of 1 to 5 regarding the operator's attitude.
timeliness | integer | yes if isNoShowRating is not true | A rating of 1 to 5 regarding the operator's timeliness.
safety | integer | yes if isNoShowRating is not true | A 1 to 5 rating of the operator's safety practices.
qualityProficiency | integer | yes if isNoShowRating is not true | A 1 to 5 rating of the operator's work quality and proficiency

> The above command returns JSON structured like this:

```json
[
    {
        "id": 10021
        , "bidSetId": null
        , "opId": 5334
        , "operatorId": 4443
        , "operatorratingId": 464
        , "businessratingId": null
        , "startTime": "2019-04-03T13:00:00.201Z"
        , "endTime": "2019-04-03T21:00:00.201Z"
        , "bidQuantity": 8
        , "isInvited": true
        , "hasScheduleConflict": false
        , "isAccepted": false
        , "isWithdrawn": false
        , "isCompleted": true
        , "isPaid": true
        , "isDisputed": false
        , "disputeCategory": null
        , "withdrawalReason": null
        , "paymentToVeryableId": null
        , "paymentToOperatorId": null
        , "premiumRateId": null
        , "isCancelled": false
        , "cancellationReason": null
        , "bidRateIncrease": null
        , "operatorOverallRating": "5.0"
        , "timelinessRating": "5.0"
        , "attitudeRating": "5.0"
        , "safetyRating": "5.0"
        , "qualityProficiencyRating": "5.0"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Bid not found. Please check the Id."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Profile

## Add Location for Business

```shell
curl -X POST "http://platform.veryableops.com/api/profile/locations?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
          "name": "New Location"
        , "isPrimary": false
        , "addressLine1": "444 American Way"
        , "addressLine2": "Suite 2"
        , "phoneNumber": "232-445-4545"
        , "city": "Dallas"
        , "state": "TX"
        , "zip": "75202" 
        }'
```

This endpoint creates a location for your business.

### HTTP Request

`POST https://platform.veryableops.com/api/profile/locations`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
name | string | yes | The name of the location being created.
isPrimary | boolean | no | Whether or not this is the primary location for your business.
addressLine1 | string | yes | The first line of the business's address.
addressLine2 | string | no | Optional second address line for suite #, apt #, etc.
phoneNumber | integer | yes | A contact # for this location.
city | string | yes | The business location's city.
state | string | yes | The abbreviation for the state. (TX, PA, etc.)
zip | string | yes | The business location's zip code.


> The above command returns JSON structured like this:

```json
[
    {
        "id": 313,
        "name": "new location (Santa Fe)",
        "isPrimary": false,
        "isRemoved": false,
        "businessId": 300,
        "contactId": 857,
        "districtId": 1,
        "addressLine1": "444 American Way",
        "addressLine2": null,
        "city": "Dallas",
        "state": "TX",
        "zip": "75202",
        "latlng": {
            "type": "Point",
            "coordinates": [
                -96.8841109,
                32.6661298
            ]
        },
        "phoneNumber": "1234567890"
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Unable to retrieve default district."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Locations for Business

```shell
curl -X GET "http://platform.veryableops.com/api/profile/locations?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets locations for your business.

### HTTP Request

`GET https://platform.veryableops.com/api/profile/locations`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 313,
        "name": "new location (Santa Fe)",
        "isPrimary": false,
        "isRemoved": false,
        "businessId": 300,
        "contactId": 857,
        "districtId": 1,
        "addressLine1": "444 American Way",
        "addressLine2": null,
        "city": "Dallas",
        "state": "TX",
        "zip": "75202",
        "latlng": {
            "type": "Point",
            "coordinates": [
                -96.8841109,
                32.6661298
            ]
        },
        "phoneNumber": "1234567890"
    },
    {
        "id": 314,
        "name": "second location (Monterrey)",
        "isPrimary": false,
        "isRemoved": false,
        "businessId": 300,
        "contactId": 857,
        "districtId": 1,
        "addressLine1": "220 American Way",
        "addressLine2": null,
        "city": "Dallas",
        "state": "TX",
        "zip": "75202",
        "latlng": {
            "type": "Point",
            "coordinates": [
                -96.8841109,
                32.6661298
            ]
        },
        "phoneNumber": "1234567890"
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Unable to retrieve default district."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Location for Business

```shell
curl -X PUT "http://platform.veryableops.com/api/profile/locations/312?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{ 
        "name": "Updated Location Name"
        , "addressLine1": "444 Canadian Way"
        , "addressLine2": "suite 222"
        , "phoneNumber": "1234567890"
        , "city": "Dallas"
        , "state": "TX"
        , "zip": "75201"
        }'
```

This endpoint updates a location for your business.

### HTTP Request

`PUT https://platform.veryableops.com/api/profile/locations/<locationId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
locationId | yes | The ID of the location to update.

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
name | string | yes | The name of the location being created.
isPrimary | boolean | yes | Whether or not this is the primary location for your business.
addressLine1 | string | yes | The first line of the business's address.
addressLine2 | string | no | Optional second address line for suite #, apt #, etc.
phoneNumber | integer | yes | A contact # for this location.
city | string | yes | The business location's city.
state | string | yes | The abbreviation for the state. (TX, PA, etc.)
zip | string | yes | The business location's zip code.



> The above command returns JSON structured like this:

```json
{
    "id": 312,
    "name": "Updated Location Name",
    "isPrimary": false,
    "isRemoved": false,
    "businessId": 300,
    "contactId": 828,
    "districtId": 1,
    "addressLine1": "444 Canadian Way",
    "addressLine2": "suite 222",
    "city": "Dallas",
    "state": "TX",
    "zip": "75201",
    "latlng": {
        "type": "Point",
        "coordinates": [
            -96.8841109,
            32.6661298
        ]
    },
    "phoneNumber": "9876543210"
}
```

> Here is an example of an error response:

```json
{
    "message": "Error retrieving timezone."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Work Areas for Business

```shell
curl -X GET "http://platform.veryableops.com/api/profile/work-areas?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets work areas associated with your business.

### HTTP Request

`GET https://platform.veryableops.com/api/profile/work-areas`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 98,
        "name": "General"
    },
    {
        "id": 231,
        "name": "Second Work Area"
    },
    {
        "id": 232,
        "name": "Third Work Area"
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error retrieving work areas."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Create Work Area for Business

```shell
curl -X POST "http://platform.veryableops.com/api/profile/work-areas?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{ "workAreas": [ "Newest Work Area" ] }'
```

This endpoint creates a work area for your business.

### HTTP Request

`POST https://platform.veryableops.com/api/profile/work-areas`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
workAreas | array[string] | yes | An array of work area names. You must pass at least one element in the array.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 233,
        "businessId": 300,
        "name": "Newest Work Area",
        "isRemoved": false,
        "createdAt": "2019-04-09T20:00:06.817Z",
        "updatedAt": "2019-04-09T20:00:06.817Z"
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Work areas param is required."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Your Labor Pool (YLP)

## Get Labor Pool for Business

```shell
curl -X GET "http://platform.veryableops.com/api/labor-pool?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets the labor pool for your business.

### HTTP Request

`GET https://platform.veryableops.com/api/labor-pool`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 316,
        "businessId": 300,
        "operatorId": 1061,
        "createdAt": "2019-02-28T21:04:35.665Z",
        "updatedAt": "2019-02-28T21:04:35.665Z"
    },
    {
        "id": 298,
        "businessId": 300,
        "operatorId": 605,
        "createdAt": "2019-01-29T16:20:09.344Z",
        "updatedAt": "2019-03-01T17:10:34.973Z"
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error getting YLP."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Toggle Operator in YLP

```shell
curl -X POST "http://platform.veryableops.com/api/labor-pool?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{"operatorId": 361, "action": "favorite"}'
```

This endpoint toggles an operator in or out of your labor pool.

### HTTP Request

`POST https://platform.veryableops.com/api/labor-pool`

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
operatorId | number | yes | The operatorId for the operator you want to toggle.
action | string | yes | You can pass "favorite" or "unfavorite".

> The above command returns JSON structured like this:

```json
{
    "message": "Operator has been favorited.",
    "favorite": [
        {
            "id": 361,
            "businessId": 300,
            "operatorId": 39328,
            "createdAt": "2019-04-09T15:55:56.259Z",
            "updatedAt": "2019-04-09T15:55:56.259Z"
        }
    ]
}
```

> Here is an example of an error response:

```json
{
    "message": "Error toggling favorite."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Toggle Block Operator

```shell
curl -X POST "http://platform.veryableops.com/api/labor-pool/block?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{"operatorId": 915}'
```

This endpoint toggles an operator from a business's block list.

### HTTP Request

`POST https://platform.veryableops.com/api/labor-pool`

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
operatorId | number | yes | The operatorId for the operator you want to toggle.

> The above command returns JSON structured like this:

```json
"Operator ID 915 has been removed from the block list of Business ID 300."
```

> Here is an example of an error response:

```json
{
    "message": "Error during block operator toggle."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Work Centers (API Config)

## Get Work Centers for Business

```shell
curl -X GET "http://platform.veryableops.com/api/workcenters?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets the work centers for your business.

### HTTP Request

`GET https://platform.veryableops.com/api/workcenters`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "name": "Lathe Workcenter"
        , "description": "..."
        , "operatorCapacity": 10
        , "unitCapacity": 10
        , "timePerUnit": 10
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-05T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error getting business work centers for business [ businessId ] - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Work Center for Business

```shell
curl -X PUT "http://platform.veryableops.com/api/workcenters/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
            "name": "My updated work center",
            "description": "Description of updated work center.",
            "operatorCapacity": 10,
            "unitCapacity": 20,
            "timePerUnit": 30,
        }'
```

This endpoint gets the work centers for your business.

### HTTP Request

`PUT https://platform.veryableops.com/api/workcenters/<workcenterId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
workcenterId | yes | The ID of the workcenter to update.

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
name | string | no | The name of the work center.
description | string | no | The description of the work center.
operatorCapacity | integer | no | The maximum number of operators that can utilize this workcenter at once.
unitCapacity | integer | no | The maximum number of units that can be produced in a work day.
timePerUnit | integer | no | The time it takes to complete one unit of product in this workcenter.

> The above command returns JSON structured like this:

```json
[
{
    "id": 4,
    "businessId": 300,
    "name": "My updated work center",
    "description": "Description of updated work center.",
    "operatorCapacity": 10,
    "unitCapacity": 20,
    "timePerUnit": 30,
    "createdAt": "2019-04-14T18:54:56.583Z",
    "updatedAt": "2019-04-14T18:54:56.583Z"
}
]
```

> Here is an example of an error response:

```json
{
    "message": "The work center was not able to be updated - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Create Work Center for Business

```shell
curl -X POST "http://platform.veryableops.com/api/workcenters?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d '${
        "name": "New Lathe Work Center",
        "description": "This is a work center description",
        "operatorCapacity": 10,
        "unitCapacity": 10,
        "timePerUnit": 10
    }'
```

This endpoint creates a work center for your business.

### HTTP Request

`POST https://platform.veryableops.com/api/workcenters`

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
name | string | no | The name of the work center.
description | string | no | The description of the work center.
operatorCapacity | integer | no | The maximum number of operators that can utilize this workcenter at once.
unitCapacity | integer | no | The maximum number of units that can be produced in a work day.
timePerUnit | integer | no | The time it takes to complete one unit of product in this workcenter.

> The above command returns JSON structured like this:

```json
[
    {
        "businessId": 300,
        "name": "New Lathe Work Center",
        "description": "This is a work center description.",
        "operatorCapacity": 10,
        "unitCapacity": 10,
        "timePerUnit": 10
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error creating new business work center row - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Delete Work Center for Business

```shell
curl -X DELETE "http://platform.veryableops.com/api/workcenters/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint deletes a work center for a business.

### HTTP Request

`DELETE https://platform.veryableops.com/api/workcenters/<workcenterId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
workcenterId | yes | The ID of the work center to delete.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "name": "Deleted Work Center"
        , "description": "This is a work center description."
        , "operatorCapacity": 10
        , "unitCapacity": 10
        , "timePerUnit": 10
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-05T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "The work center was not able to be deleted. - [errMessage]"
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Business Customers (API Config)

## Get Customers for Business

```shell
curl -X GET "http://platform.veryableops.com/api/customers?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets customers for your business.

### HTTP Request

`GET https://platform.veryableops.com/api/customers`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "customerName": "Our Customer"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error getting business customers for business [businessId] - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Customer for Business

```shell
curl -X PUT "http://platform.veryableops.com/api/customers/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
        "customerName": "Our Updated Customer"
    }'
```

This endpoint updates a customer for your business.

### HTTP Request

`PUT https://platform.veryableops.com/api/customers/<customerId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
customerId | yes | The ID of the customer to update.

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
customerName | string | yes | The name of the business customer.


> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "customerName": "Our Updated Customer"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "The business customer was not able to be updated. - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Create Customer for Business

```shell
curl -X POST "http://platform.veryableops.com/api/customers?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
        "customerName": "Our Customer"
    }'
```

This endpoint creates a customer for your business.

### HTTP Request

`POST https://platform.veryableops.com/api/customers`

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
customerName | string | yes | The name of the business customer.


> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "customerName": "Our Customer"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error creating new business customers row - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Delete Customer for Business

```shell
curl -X DELETE "http://platform.veryableops.com/api/customers/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint deletes a customer for your business.

### HTTP Request

`DELETE https://platform.veryableops.com/api/customers/<customerId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
customerId | yes | The ID of the customer to delete.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "customerName": "Our Deleted Customer"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "The business customer was not able to be deleted. - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Production Schedules (API Config)

## Get Production Schedules for Business

```shell
curl -X GET "http://platform.veryableops.com/api/schedules?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets production schedules for your business.

### HTTP Request

`GET https://platform.veryableops.com/api/schedules`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error getting business production schedules for business [businessId] - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Create Production Schedules for Business

```shell
curl -X POST "http://platform.veryableops.com/api/schedules?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint creates a production schedule for your business.

### HTTP Request

`POST https://platform.veryableops.com/api/schedules`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error creating business production schedule for business [businessId] - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Delete Production Schedule for Business

```shell
curl -X DELETE "http://platform.veryableops.com/api/schedules/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint creates a production schedule for your business.

### HTTP Request

`DELETE https://platform.veryableops.com/api/schedules/<scheduleId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
scheduleId | yes | The ID of the schedule to delete.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "The business schedule was not able to be deleted. - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Routings (API Config)

## Get Routings for Business

```shell
curl -X GET "http://platform.veryableops.com/api/routings?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets the routings for your business.

### HTTP Request

`GET https://platform.veryableops.com/api/routings`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "businesscontactId": 163
        , "businessworkareaId": 98
        , "name": "Primary Routing System"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error getting business routings for business [ businessId ] - [ errorMessage ]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Routing for Business

```shell
curl -X PUT "http://platform.veryableops.com/api/routings/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
        "name": "Secondary Routing System"
    }'
```

This endpoint updates a routing for your business.

### HTTP Request

`PUT https://platform.veryableops.com/api/routings/<routingId>`

### URL Parameters

Parameter | Required | Description
--------- | ---- | -----------
routingId | yes | The ID of routing to update.

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
name | string | yes | The updated name of the routing.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "businesscontactId": 163
        , "businessworkareaId": 98
        , "name": "Secondary Routing System"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Routing was not able to be updated - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Create Routing for Business

```shell
curl -X POST "http://platform.veryableops.com/api/routings?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
        "name": "New Routing System",
        "businesscontactId" 163,
        "businessWorkareaId": 98
    }'
```

This endpoint creates a routing for your business.

### HTTP Request

`POST https://platform.veryableops.com/api/routings`

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
name | string | yes | The name of the routing.
businesscontactId | integer | yes | The contact Id for your business.
businessWorkareaId | integer | yes | The work area for your business.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "businesscontactId": 163
        , "businessworkareaId": 98
        , "name": "New Routing System"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error creating new business routings row - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Delete Routing for Business

```shell
curl -X DELETE "http://platform.veryableops.com/api/routings?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint deletes a routing for a business.

### HTTP Request

`DELETE https://platform.veryableops.com/api/routings/<routingId>`

### URL Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
routingId | intger | yes | The Id for the routing to be deleted.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "businesscontactId": 163
        , "businessworkareaId": 98
        , "name": "Deleted Routing System"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Routing was not able to be deleted - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# SKUs (API Config)

## Get SKUs for Business

```shell
curl -X GET "http://platform.veryableops.com/api/skus?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint gets SKUs for a business.

### HTTP Request

`GET https://platform.veryableops.com/api/skus`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "sku": "GFDA46RERTE4"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-05T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error getting business SKUs for business [ businessId ] - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update SKU for Business

```shell
curl -X PUT "http://platform.veryableops.com/api/skus/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{"sku": "3542KD435"}'
```

This endpoint updates a SKU for a business.

### HTTP Request

`PUT https://platform.veryableops.com/api/skus/<skuId>`

### URL Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
skuId | integer | yes | The Id for the SKU to update.

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
sku | string | yes | The Stock Keeping Unit for a product.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "sku": "3542KD435"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-05T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error updating SKU - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Create SKU for Business

```shell
curl -X POST "http://platform.veryableops.com/api/skus?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{"sku": 55FFADG34}'
```

This endpoint creates a SKU for a business.

### HTTP Request

`POST https://platform.veryableops.com/api/skus/<skuId>`

### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
sku | string | yes | The Stock Keeping Unit for a product.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "sku": "55FFADG34"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-05T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error creating new business SKU row - [errorMessage]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Delete SKU for Business

```shell
curl -X DELETE "http://platform.veryableops.com/api/skus/1?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint deletes a SKU for a business.

### HTTP Request

`DELETE https://platform.veryableops.com/api/skus/<skuId>`

### URL Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
skuId | integer | yes | The Id for the SKU to be deleted.

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1
        , "businessId": 300
        , "sku": "55FFADG34"
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-05T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error deleting SKU - [ errorMessage ]."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Events

## Events Introduction
When specific events occur on the Veryable platform, we create a new event resource to document the change. When an event resource is created, webhooks will be created and sent for active webhook subscriptions.


## Get Events

```shell
curl -X "GET" "https://platform.verableops.com/api/events/?businessId=300" 
      -H 'Authorization: bearer [JWT Token]' 
```

This endpoint retrieves all events of a business.


### HTTP Request

`GET https://platform.veryableops.com/api/events`


> The above command returns JSON structured like this:

```json
[
  {
    "id": 60,
    "platformEventId": 253,
    "createdAt": "2019-04-15T19:40:08.008Z",
    "data": {
      "id": 324,
      "zip": "75202",
      "city": "Dallas",
      "name": "Updated Location Here",
      "state": "TX",
      "latlng": {
        "type": "Point",
        "coordinates": [
          -96.8042882,
          32.7774686
        ]
      },
      "contactId": 880,
      "isPrimary": false,
      "isRemoved": false,
      "businessId": 300,
      "districtId": 1,
      "phoneNumber": "(123) 456-7890",
      "addressLine1": "888 Huskell Drive",
      "addressLine2": null
    }
  }
]
```
> Here is an example of an error response:

```json
{
    "message": "Error retrieving events."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Event

```shell
curl -X "PUT" "https://platform.verableops.com/api/events/<eventId>?businessId=300" 
      -H 'Authorization: bearer [JWT Token]' 
      -d $'{
  "userId": "927",
  "data": {
    "dataProperty": "updated data information"
  },
  "platformEventId": "3"
}'
```

This endpoint retrieves all events of a business.


### HTTP Request

`PUT https://platform.veryableops.com/api/events/<eventId>`

### URL Parameters 
Parameter | Required | Description
--------- | ---- | -----------
eventId | yes | The ID of the event.


### Body Parameters
Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
userId | integer | no | The Id of the user.
platformEventId | integer | no | The Id of the platform event.
data | object | no | The data of the event.


> The above command returns JSON structured like this:

```json
[
  {
    "id": 8,
    "platformEventId": 3,
    "createdAt": "2019-04-12T19:37:01.867Z",
    "data": {
      "dataProperty": "new data of event"
    }
  }
]
```
> Here is an example of an error response:

```json
{
    "message": "Error updating event."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Platform Events

```shell
curl -X "GET" "https://platform.verableops.com/api/events/platformevents?businessId=727" 
      -H 'Authorization: bearer [JWT Token]' 
```

This endpoint retrieves all platform events that can be subscribed to. 


### HTTP Request

`GET https://platform.veryableops.com/api/events/platformevents`


> The above command returns JSON structured like this:

```json
[
  {
    "id": 161,
    "platformEventName": "Op reactivated"
  },
  {
    "id": 255,
    "platformEventName": "Bid disputed"
  },
  {
    "id": 248,
    "platformEventName": "Operator rated multiple"
  },
  {
    "id": 249,
    "platformEventName": "Operator added to labor pool"
  },
  {
    "id": 250,
    "platformEventName": "Operator removed from labor pool"
  },
  {
    "id": 251,
    "platformEventName": "Operator blocked from business"
  },
  {
    "id": 252,
    "platformEventName": "Business location added"
  },
  {
    "id": 253,
    "platformEventName": "Business location updated"
  },
  {
    "id": 254,
    "platformEventName": "Work area added"
  },
  {
    "id": 271,
    "platformEventName": "Op cancelled"
  },
  {
    "id": 272,
    "platformEventName": "Operator assignment cancelled"
  },
  {
    "id": 16,
    "platformEventName": "Op updated"
  },
  {
    "id": 24,
    "platformEventName": "Bid adjusted"
  },
  {
    "id": 9,
    "platformEventName": "Operator rated"
  },
  {
    "id": 160,
    "platformEventName": "Op deactivated"
  },
  {
    "id": 18,
    "platformEventName": "Op created"
  },
  {
    "id": 7,
    "platformEventName": "Bid accepted"
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error retrieving platform events."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Webhooks

## Webhooks Introduction
Whenever an event occurs that is related to your application, Veryable sends a POST request to your designated Webhook URL that includes information of the event that occured. 

In order to receive webhooks, you'll need to set up a webhook subscription.

## Responding to webhooks
When you receive a webhook, your endpoint should return a HTTP status code of 200. 

If Veryable does not receive a HTTP status code of 200, we will immediately retry three times. If those retries fail, we will continue to retry every hour up to twelve total retries. 

## Securing webhooks
For security reasons, we pass along a hash signature with each webhook request in the header **x-veryable-signature**. 

When you receive the webhook request, you can verify that the request came from Veryable by computing your own hash and comparing it to the hash in the **x-veryable-signature** header.

The hash signature is generated with the HMAC algorithm, passing in the stringified request body and using your API secret as a key and the SHA256 digest mode.


## Get Webhooks


```shell
curl -X "GET" "https://platform.verableops.com/api/webhooks?subscriptionId=1&businessId=300" 
      -H 'Authorization: bearer [JWT Token]' 
```

This endpoint retrieves all webhooks for a subscription.


### HTTP Request

`GET https://platform.veryableops.com/api/webhooks`


### Query Parameters 

Parameter | Required | Description
--------- | ---- | -----------
subscriptionId | yes | The ID of the subscription.


> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "eventId": 32,
    "createdAt": "2019-04-15T16:58:44.626Z",
    "subscriptionId": 1
  },
  {
    "id": 2,
    "eventId": 36,
    "createdAt": "2019-04-15T18:39:29.600Z",
    "subscriptionId": 1
  },
  {
    "id": 3,
    "eventId": 37,
    "createdAt": "2019-04-15T18:50:11.172Z",
    "subscriptionId": 1
  },
  {
    "id": 4,
    "eventId": 38,
    "createdAt": "2019-04-15T18:50:43.658Z",
    "subscriptionId": 1
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error retrieving webhooks."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>


# Webhook Subscriptions

## Subscription Introduction
In order to receive webhooks, you will need to subscribe to the desired business and its events. When you create a subscription, it automatically listens for all webhook enabled platform events. You can also customize which platform events your subscriptions listen to. 



## Get Webhook Subscriptions


```shell
curl -X "GET" "https://platform.verableops.com/api/webhook-subscriptions?businessId=727" 
      -H 'Authorization: bearer [JWT Token]' 
```

This endpoint retrieves all webhook subscriptions for an organization.

### HTTP Request

`GET https://platform.veryableops.com/api/webhook-subscriptions`

> The above command returns JSON structured like this:

```json
[
  {
    "id": 4,
    "businessId": 300,
    "recipientUrl": "https://yourcompany.com/api/webhooks",
    "createdAt": "2019-04-16T18:33:09.130Z",
    "httpMethod": "POST"
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error retrieving webhook subscriptions."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>


## Add Webhook Subscription


```shell
curl -X "POST" "https://platform.verableops.com/api/webhook-subscriptions?businessId=727" 
      -H 'Authorization: bearer [JWT Token]' 
        -d $'{
          "isActive": "true",
          "httpMethod": "post",
          "recipientUrl": "https://yourcompany.com/api/webhooks",
          "organizationId": "3"
          }'
```
This endpoint creates a webhook subscription for an organization.

### HTTP Request

`POST https://platform.veryableops.com/api/wehook-subscriptions`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
recipientUrl | string | yes | The Url for receiving webhooks.
isActive | boolean | yes | The active status of subscription.
httpMethod | string | yes | The http method for receiving webhooks.
organizationId | integer | yes | The id of the organization adding a subscription.


> The above command returns JSON structured like this:

```json
[
  {
    "id": 5,
    "businessId": 300,
    "recipientUrl": "https://yourcompany.com/api/webhooks",
    "createdAt": "2019-04-16T22:38:29.059Z",
    "httpMethod": "post"
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error adding webhook subscription."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Webhook Subscription


```shell
curl -X "PUT" "https://platform.verableops.com/api/webhook-subscriptions/<subscriptionId>?businessId=300" 
      -H 'Authorization: bearer [JWT Token]' 
      -d $'{
          "httpMethod": "post",
          "recipientUrl": "https://yourcompany.com/api/webhooks,
          "isActive": true
        }'
```
This endpoint updates a webhook subscription for an organization. It is also a toggle to turn on/off a subscription.

### HTTP Request

`PUT https://platform.veryableops.com/api/wehook-subscriptions/<subscriptionId>`

### URL Parameters 
Parameter | Required | Description
--------- | ---- | -----------
subscriptionId | yes | The ID of the subscription.

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
recipientUrl   | string | no | The Url for receiving webhooks.
isActive | boolean | no | The active status of subscription.
httpMethod | string | no | The http method for receiving webhooks.


> The above command returns JSON structured like this:

```json
[
  {
    "id": 5,
    "businessId": 300,
    "recipientUrl": "https://yourcompany.com/api/webhooks",
    "createdAt": "2019-04-16T22:38:29.059Z",
    "httpMethod": "post"
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error updating webhook subscription."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

<!-----------------> 

# Webhook Subscriptions Events

## Get Webhook Subscription Events


```shell
curl -X "GET" "https://platform.verableops.com/api/webhook-subscriptions/subscriptionevent?businessId=727" 
      -H 'Authorization: bearer [JWT Token]' 
```

This endpoint retrieves all webhook subscription events for an organization.

### HTTP Request

`GET https://platform.veryableops.com/api/webhook-subscriptions/subscriptionevent`

> The above command returns JSON structured like this:

```json
[
  {
    "webhooksubscriptionId": 3,
    "platformEventId": 161,
    "recipientUrl": "https://yourcompany.com/api/webhooks",
    "isActive": true,
    "httpMethod": "POST"
  },
  {
    "webhooksubscriptionId": 3,
    "platformEventId": 255,
    "recipientUrl": "https://yourcompany.com/api/webhooks",
    "isActive": true,
    "httpMethod": "POST"
  },
  {
    "webhooksubscriptionId": 3,
    "platformEventId": 248,
    "recipientUrl": "https://yourcompany.com/api/webhooks",
    "isActive": true,
    "httpMethod": "POST"
  },
  {
    "webhooksubscriptionId": 3,
    "platformEventId": 249,
    "recipientUrl": "https://yourcompany.com/api/webhooks",
    "isActive": true,
    "httpMethod": "POST"
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error retrieving webhook subscription events."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Add Webhook Subscription Event

```shell
curl -X "POST" "https://platform.verableops.com/api/webhook-subscriptions/subscriptionevent?businessId=300" 
      -H 'Authorization: bearer [JWT Token]' 
      -d $'{
          "platformEventId": "7",
          "webhookSubscriptionId": "6"
        }'

```
This endpoint adds a webhook subscription event for an organization's webhook subscription.

### HTTP Request

`POST https://platform.veryableops.com/api/wehook-subscriptions/subscriptionevent`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
platformEventId | integer | yes | The Id of the platform event.
webhookSubscriptionId | integer | yes | The Id of the organization's webhook subscription.


> The above command returns JSON structured like this:

```json
[
  {
    "id": 91,
    "webhooksubscriptionId": 6,
    "platformEventId": 7
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error adding webhook subscription event."
}

```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Toggle Webhook Subscription Event

```shell
curl -X POST "https://platform.verableops.com/api/webhook-subscriptions/subscriptionevent/toggle?businessId=300"
    -H "Authorization: Bearer [JWT string]"
    -d $'{
        "platformEventId": 16,
        "webhookSubscriptionId": 5
      }'
```

This endpoint toggles webhook subscription events for a subscription. It toggles to add or delete the subscription event. 

### HTTP Request

`POST https://platform.veryableops.com/api/webhook-subscriptions/subscriptionevent/toggle`

### Body Parameters

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
platformEventId | integer | yes | The Id of the platform event.
webhookSubscriptionId | integer | yes | The Id of the organization's webhook subscription.


> The above command returns JSON structured like this:

```json
[
  {
    "id": 91,
    "webhooksubscriptionId": 6,
    "platformEventId": 7
  }
]
```

> Here is an example of an error response:

```json
{
    "message": "Error toggling webhook subscription event."
}
```

<aside class="warning">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>



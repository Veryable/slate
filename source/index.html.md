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
https://platform.veryableops.com/api/dummyendpoint?businessId=226
```

<aside class="notice">
In addition, a business ID (corresponding to a business you have access to) must be passed as a <code>businessId</code> query parameter with every request, formatted like the example to the right.
</aside>

# Bids

## Get Bids For Op

```shell
curl -X GET "http://localhost:3000/api/bids\?businessId=226&opId=6134"
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
{
  "message": "Bids have successfully been retrieved.",
  "bids": [
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
}
```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Bid By ID

```shell
curl -X GET "http://localhost:3000/api/bids/101933\?businessId=226"
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
{
  "message": "Bid has successfully been retrieved.",
  "bid": [
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
}
```

<aside class="warning">Make sure you lower the font size prior to submitting your request.</aside>

## Adjust Bid By ID

```shell
curl -X "PUT" "http://localhost:3000/api/bids/<bidId>/adjust?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
     -d $'{"bidQuantity": 6}'
```

This endpoint adjusts the bid quantity of a specific bid by ID.

### HTTP Request

`GET https://platform.veryableops.com/api/bids/<bidId>/adjust`

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
  "message": "Bid(s) adjusted.",
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

# Ops

## Get Op By Id

```shell
curl -X GET "http://localhost:3000/api/ops/<opId>/?businessId=300"
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
        , "multidayEndDate": NULL
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill" NULL
        , "opQuantity": 8
        , "filledQuantity": 8
        , multidayWorkWeek: ['Monday', 'Tuesday']
        , isInactive: NULL
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": TRUE
        , "isCompleted": FALSE
        , "isPoolOnly": FALSE
        , "bidSetId": NULL
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

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Ops For Business

```shell
curl -X GET "http://localhost:3000/api/ops/business/all/?businessId=300"
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
        , "multidayEndDate": NULL
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill" NULL
        , "opQuantity": 8
        , "filledQuantity": 8
        , multidayWorkWeek: ['Monday', 'Tuesday']
        , isInactive: NULL
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": TRUE
        , "isCompleted": FALSE
        , "isPoolOnly": FALSE
        , o.bidSetId: NULL
        , o.bidSetIds: []
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
        , "multidayEndDate": NULL
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill" NULL
        , "opQuantity": 8
        , "filledQuantity": 8
        , multidayWorkWeek: ['Monday', 'Tuesday']
        , isInactive: NULL
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": TRUE
        , "isCompleted": FALSE
        , "isPoolOnly": FALSE
        , o.bidSetId: NULL
        , o.bidSetIds: []
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

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Update Op

```shell
curl -X PUT "http://localhost:3000/api/ops/<id>/?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
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
        , "opDescription": "Description of the op."
        , "opDate": "2019-03-21T13:00:00.000Z"
        , "earliestStartTime": "2019-03-21T13:00:00.000Z"
        , "latestStartTime": "2019-03-21T13:00:00.000Z"
        , "multidayEndDate": NULL
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill" NULL
        , "opQuantity": 8
        , "filledQuantity": 8
        , multidayWorkWeek: ['Monday', 'Tuesday']
        , isInactive: NULL
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": TRUE
        , "isCompleted": FALSE
        , "isPoolOnly": FALSE
        , o.bidSetId: NULL
        , o.bidSetIds: []
        , "contactPerson": "Peggy Gou"
        , "businessworkareaId": 44
        , "businesscontactId": 3
        , "publicId": "19-52"
        , "createdAt": 2019-03-05T16:34:10.201Z
        , "updatedAt": 2019-03-06T16:34:10.201Z 
    }
]
```

> Here is an example of an error response:

```json
{
    message: "The op you requested could not be retrieved."
}

```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Post Op

```shell
curl -X POST "http://localhost:3000/api/ops/?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
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
        "id": 1235
        , "businessId": 300
        , "title": "My New Op"
        , "opDescription": "My op description."
        , "opDate": "2019-03-21T13:00:00.000Z"
        , "earliestStartTime": "2019-03-21T13:00:00.000Z"
        , "latestStartTime": "2019-03-21T13:00:00.000Z"
        , "multidayEndDate": NULL
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill" NULL
        , "opQuantity": 8
        , "filledQuantity": 0
        , isInactive: NULL
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": TRUE
        , "isCompleted": FALSE
        , "isPoolOnly": FALSE
        , "bidSetId": NULL
        , "bidSetIds": []
        , "contactPerson": "Peggy Gou"
        , "businessworkareaId": 44
        , "businesscontactId": 3
        , "opcontactId": 5
        , "publicId": "19-52"
        , "createdAt": 2019-03-05T16:34:10.201Z
        , "updatedAt": 2019-03-06T16:34:10.201Z 
    }
]
```

> Here is an example of an error response:

```json
{
    message: "This company cannot create a new Op, as it currently has Op(s) that are incomplete and past their grace period."
}

```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Deactivate Op

```shell
curl -X DELETE "http://localhost:3000/api/ops<opId>/?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint deactivates an op that doesn't have accepted bids.

### HTTP Request

`DELETE https://platform.veryableops.com/api/ops<opId>`

> The above command returns JSON structured like this:

```json
[
    {
        "id": 1235
        , "businessId": 300
        , "title": "Op Title 2"
        , "opDescription": "Description of the op."
        , "opDate": "2019-03-21T13:00:00.000Z"
        , "earliestStartTime": "2019-03-21T13:00:00.000Z"
        , "latestStartTime": "2019-03-21T13:00:00.000Z"
        , "multidayEndDate": NULL
        , "break_hours": 1
        , "rally_point": "Front Gate"
        , "autofill" NULL
        , "opQuantity": 8
        , "filledQuantity": 8
        , multidayWorkWeek: ['Monday', 'Tuesday']
        , isInactive: NULL
        , "optermsId": 1
        , "opContactId": 5
        , "isFulfilled": TRUE
        , "isCompleted": FALSE
        , "isPoolOnly": FALSE
        , "bidSetId": NULL
        , "bidSetIds": []
        , "contactPerson": "Peggy Gou"
        , "businessworkareaId": 44
        , "businesscontactId": 3
        , "opcontactId": 65
        , "publicId": "19-52"
        , "createdAt": 2019-03-05T16:34:10.201Z
        , "updatedAt": 2019-03-06T16:34:10.201Z 
    }
]
```

> Here is an example of an error response:

```json
{
    message: "This company cannot create a new Op, as it currently has Op(s) that are incomplete and past their grace period."
}

```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

<!-- REACTIVATE BUSINESS GOES HERE -->

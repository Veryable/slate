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

# Ops

## Cancel Op

```shell
curl -X "PUT" "http://localhost:3000/api/ops/11529/cancel?businessId=226"
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
      "bidSetId": null,
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
curl -X GET "http://localhost:3000/api/bids/<bidId>\?businessId=226"
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
curl -X "PUT" "http://localhost:3000/api/bids/101933/adjust?businessId=226"
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

## Adjust Multiple Bids

```shell
curl -X "PUT" "http://localhost:3000/api/bids/adjust?businessId=226"
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
  "message": "Bid(s) adjusted.",
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

## Accept Bid

```shell
curl -X "PUT" "http://localhost:3000/api/bids/101933/accept?businessId=226"
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
{
  "message": "Bid accepted.",
  "bid": [
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
}
```

## Dispute Bid

```shell
curl -X "PUT" "http://localhost:3000/api/bids/<bidId>/dispute?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
     -d $'{
          "category": "other",
          "comment": "Operator failed to follow protocol."
        }'
```

This endpoint disputes a bid.

### HTTP Request

`PUT https://platform.veryableops.com/api/bids/101933/dispute`

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
{
  "message": "Bid disputed.",
  "bid": [
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
}
```

# Ops

## Get Op By Id

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
        , "multidayWorkWeek": ['Monday', 'Tuesday']
        , "isInactive": NULL
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
        , "multidayWorkWeek": ['Monday', 'Tuesday']
        , "isInactive": NULL
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
        , "multidayWorkWeek": ['Monday', 'Tuesday']
        , "isInactive": NULL
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
        , "isInactive": NULL
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
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z"
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
curl -X DELETE "http://localhost:3000/api/ops/<opId>/?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint deactivates an op that doesn't have accepted bids.

### HTTP Request

`DELETE https://platform.veryableops.com/api/ops/<opId>`

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
        , "multidayWorkWeek": ['Monday', 'Tuesday']
        , "isInactive": NULL
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
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
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

## Reactivate Op

```shell
curl -X PUT "http://localhost:3000/api/ops/reactivate/<opId>/?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
```

This endpoint reactivates a previously deactivated op.

### HTTP Request

`PUT https://platform.veryableops.com/api/reactivate/<opId>`

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
        , "multidayWorkWeek": ['Monday', 'Tuesday']
        , "isInactive": NULL
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
        , "createdAt": "2019-03-05T16:34:10.201Z"
        , "updatedAt": "2019-03-06T16:34:10.201Z" 
    }
]
```

> Here is an example of an error response:

```json
{
    message: "Error finding op to reactivate."
}

```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get All Op Contacts for Business

```shell
curl -X GET "http://localhost:3000/api/ops/opcontacts/?=businessId=300"
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
        , "phone": "(343) 435-6643"
        , "createdAt": "2018-10-19T17:06:43.555Z"
        , "updatedAt": "2018-10-19T17:06:43.555Z"
        , "isRemoved": FALSE
        ,"phoneExt": NULL
    }

    , {
        "id": 3
        , "businessId": 300
        , "firstName": "Shamus"
        , "lastName": "O'Hoolihan"
        , "phone": "(455) 455-4545"
        , "createdAt": "2019-03-21T19:32:43.475Z"
        , "updatedAt": "2019-03-21T19:32:43.475Z"
        , "isRemoved": FALSE
        , "phoneExt": NULL
    }
]
```

> Here is an example of an error response:

```json
{
    message: "Error getting op contacts for business."
}

```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Add Op Contact for Business

```shell
curl -X POST "http://localhost:3000/api/ops/opcontacts/?=businessId=300"
    -H "Authorization: Bearer [JWT string]"
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
        , "businessId":300
        , "firstName":"Johnny"
        , "lastName":"Smith"
        , "phone":"(343) 435-6643"
        , "createdAt":"2018-10-19T17:06:43.555Z"
        , "updatedAt":"2018-10-19T17:06:43.555Z"
        , "isRemoved":FALSE
        ,"phoneExt":NULL
    }
]
```

> Here is an example of an error response:

```json
{
    message: "Error adding new op contact for business."
}

```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Toggle Op Contact for Business

```shell
curl -X PUT "http://localhost:3000/api/ops/opcontacts/?=businessId=300"
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
        , "businessId":300
        , "firstName":"Johnny"
        , "lastName":"Smith"
        , "phone":"(343) 435-6643"
        , "createdAt":"2018-10-19T17:06:43.555Z"
        , "updatedAt":"2018-10-19T17:06:43.555Z"
        , "isRemoved": TRUE
        ,"phoneExt": NULL
    }
]
```

> Here is an example of an error response:

```json
{
    message: "Error toggling op contact."
}
```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Operators

## Get Operators By Id

```shell
curl -X POST "http://localhost:3000/api/operators/?=businessId=300"
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
        , "lastActive": NULL
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": TRUE
        , "isVeteran": FALSE
        , "isDrugScreenPassed": TRUE
        , "district": "TX-1"
        , "isSuspended": FALSE
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
        , "lastActive": NULL
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": TRUE
        , "isVeteran": FALSE
        , "isDrugScreenPassed": TRUE
        , "district": "TX-1"
        , "isSuspended": FALSE
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
]
```

> Here is an example of an error response:

```json
{
    message: "You must pass at least one value inside batchOperatorIds."
}
```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

## Get Operators By Filter

```shell
curl -X POST "http://localhost:3000/api/operators/filter/?=businessId=300"
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
        , "lastActive": NULL
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": TRUE
        , "isVeteran": FALSE
        , "isDrugScreenPassed": TRUE
        , "district": "TX-1"
        , "isSuspended": FALSE
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
        , "lastActive": NULL
        , "createdAt": "2018-02-26T17:51:03.774Z"
        , "isSpanishSpeaking": TRUE
        , "isVeteran": FALSE
        , "isDrugScreenPassed": TRUE
        , "district": "TX-1"
        , "isSuspended": FALSE
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
]
```

> Here is an example of an error response:

```json
{
    message: "businesscontactId is required when filtering by maxMilesAway."
}
```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>

# Ratings

## Post Operator Rating

```shell
curl -X POST "http://localhost:3000/api/ratings/?=businessId=300"
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
isNoShowRating | boolean | no | Passing TRUE will generate a 1 star rating for each rating category.
attitude | integer | yes if isNoShowRating is not TRUE | A rating of 1 to 5 regarding the operator's attitude.
timeliness | integer | yes if isNoShowRating is not TRUE | A rating of 1 to 5 regarding the operator's timeliness.
safety | integer | yes if isNoShowRating is not TRUE | A 1 to 5 rating of the operator's safety practices.
qualityProficiency | integer | yes if isNoShowRating is not TRUE | A 1 to 5 rating of the operator's work quality and proficiency

> The above command returns JSON structured like this:

```json
[
    {
        "id": 10021
        , "bidSetId": NULL
        , "opId": 5334
        , "operatorId": 4443
        , "operatorratingId": 464
        , "businessratingId": NULL
        , "startTime": "2019-04-03T13:00:00.201Z"
        , "endTime": "2019-04-03T21:00:00.201Z"
        , "bidQuantity": 8
        , "isInvited": TRUE
        , "hasScheduleConflict": FALSE
        , "isAccepted": FALSE
        , "isWithdrawn": FALSE
        , "isCompleted": TRUE
        , "isPaid": TRUE
        , "isDisputed": FALSE
        , "disputeCategory": NULL
        , "withdrawalReason": NULL
        , "paymentToVeryableId": NULL
        , "paymentToOperatorId": NULL
        , "premiumRateId": NULL
        , "isCancelled": FALSE
        , "cancellationReason": NULL
        , "bidRateIncrease" NULL
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
    message: "Bid not found. Please check the Id."
}
```

<aside class="success">
Remember — include <code>businessId</code> as part of the query parameters!
</aside>







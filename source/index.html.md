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

# Messages

## Send Message

```shell
curl -X "POST" "http://localhost:3000/api/messages?businessId=226" \
     -H 'Authorization: bearer [JWT Token]' \
     -d $'{
          "subject": "Testing public API message engine",
          "body": "Please ignore. Thanks!",
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
  "message": "All messages sent successfully.",
  "results": [
    {
      "id": "<20190410185411.1.9FA077F09C3BD365@mg.veryableops.com>",
      "message": "Queued. Thank you."
    },
    [
      {
        "from": "+12147618335",
        "to": "+19034524698",
        "status": "queued",
        "sid": "SM76221358b8ab4b5893737de53b10b817"
      }
    ],
    [
      {
        "id": "16cfdf72-711c-4574-9fbd-f69428020ceb",
        "recipients": 1,
        "external_id": null
      }
    ],
    [
      {
        "userId": 128,
        "businessId": null,
        "id": 125274,
        "playerId": "3638d01c-db2b-4553-93a9-3b109ac48135"
      }
    ]
  ]
}
```

<aside class="warning">Make sure you are passing the correct <code>businessId</code> in your query parameters so that the API retrieves the correct sender info.</aside>
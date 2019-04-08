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

## Cancel Bid

```shell
curl -X "PUT" "http://localhost:3000/api/bids/<bidId>/cancel?businessId=226"
     -H 'Authorization: Bearer [JWT token]'
     -d $'{
          "cancellationReason": "Project has been completed, operator no longer needed."
        }'
```

This endpoint cancels a bid.

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
      "isCompleted": false,
      "isPaid": false,
      "isWithdrawn": false,
      "withdrawalReason": null,
      "isDisputed": false,
      "disputeCategory": null,
      "disputeComment": null,
      "isCancelled": true,
      "cancellationReason": "Project has been completed, operator is no longer needed.",
      "createdAt": "2019-04-04T22:16:40.850Z",
      "updatedAt": "2019-04-05T19:15:57.930Z"
    }
  ],
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
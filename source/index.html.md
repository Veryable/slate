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

Parameter | Type | Required | Description
--------- | ------ | ---- | -----------
opId | string | yes | The ID of the Op.

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

Parameter | Description
--------- | -----------
bidId | The ID of the bid to retrieve.

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

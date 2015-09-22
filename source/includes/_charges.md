# Charges

## Get All Charges

```javascript
qp.getCharges().then(function(response) { console.log(response.data) });
```
```shell
curl https://gateway.quaypay.com/api/v2/charges \
    -H "Authorization: Bearer f3ab55c097727130fdc183529131fadd4b36b7ec23fc968a7d776e56468f7134"
```
```json
{
  "total": 1,
  "results": [
    {
      "id": "charge_1-11B",
      "amount": "1000",
      "application_id": "testappid",
      "card_id": "72da85b5fd46a356aa356b7d30cd88660bf",
      "committed": true,
      "created_at": 1439170291,
      "live": false,
      "metadata": {},
      "paid": true,
      "points": false,
      "points_used": 0,
      "shipping": {},
      "user_id": "user_1-1J",
      "token": "lxuuqrLprOESO/fVH4c0aA==↵"
    }
  ]
}
```

Retrieves all charges associated with the authenticated account.

A merchant may retreive all charges associated with their application.

A customer may retreive all charges associated with their user account.

### HTTP Request

`GET https://gateway.quaypay.com/api/v2/charges`

### Return Values

Parameter | Type | Description
--------- | ------- | -----------
total | Number | The number of records returned.
results | Array | The array of charges.


## Get a Specific Charge

```javascript
qp.getCharge('charge_1-11B').then(function(response) { console.log(response.data) });
```

```json
{
  "charge": {
    "id": "charge_1-11B",
    "amount": "1000",
    "application_id": "testappid",
    "card_id": "72da85b5fd46a356aa356b7d30cd88660bf",
    "committed": true,
    "created_at": 1439170291,
    "live": false,
    "metadata": {},
    "paid": true,
    "points": false,
    "points_used": 0,
    "shipping": {},
    "user_id": "user_1-1J",
    "token": "lxuuqrLprOESO/fVH4c0aA==↵"
  }
}
```


Retrieve a specific charge.


### HTTP Request

`GET https://gateway.quaypay.com/api/v2/charges/:id`

### Return Values

Parameter | Type | Description
--------- | ---- | ---------
charge | Object | The charge associated with the ID passed in.


## Add a Charge

> Passing in a card ID accessible via qp.getCards()

```javascript
qp.addCharge({ 
    amount: '2000',
    card_id: '72da85b5fd46a356aa356b7d30cd88660bf',
    metadata: {
      product: {
        id: '9851712424',
        quantity: 3
      }
    }
  });
```

> Passing in card details directly

```javascript
qp.addCharge({ 
    amount: '2000',
    card: {
      name: 'Bob Smith',
      number: '4242 4242 4242 4242',
      exp_month: '6',
      exp_year: '2016',
      cvc: '100'    
    },
    metadata: {
      product_id: '9851712424',
      quantity: 3
    }
  });
```

```json
{
  "token": "lxuuqrLprOESO/fVH4c0aA==↵"
}
```
Add a charge using the ID of the customer's card or passing in the card details directly.

The process of retreiving a customer's stored cards, displaying those cards and charging the selected card is best handled by the <a href="#charge">Charge Workflow</a>.


### HTTP Request

`POST https://gateway.quaypay.com/api/v2/charges`

### Return Values

Parameter | Type | Description
--------- | ---- | ---------
token | string | A token that can be used to commit the charge at any time.



## Commit a Charge

> Passing in a card ID accessible via qp.getCards()

```javascript
qp.commitCharge({ 
    token: "lxuuqrLprOESO/fVH4c0aA==↵"
  });
```
```json
{
  "charge": {
    "id": "charge_1-11B",
    "amount": "2000",
    "application_id": "testappid",
    "card_id": "72da85b5fd46a356aa356b7d30cd88660bf",
    "committed": true,
    "created_at": 1439170291,
    "live": false,
    "metadata": {},
    "paid": true,
    "points": false,
    "points_used": 0,
    "shipping": {},
    "user_id": "user_1-1J",
    "token": "lxuuqrLprOESO/fVH4c0aA==↵"
  }
}
```

QuayPay uses a two-phase commit to ensure atomicity and validity of all charges.

When a charge is added by a customer, the token returned is used to 'commit' that charge. This can be done either on the merchant's server side using the application secret, or by the authenticated account who created the initial charge.



### HTTP Request

`POST https://gateway.quaypay.com/api/v2/charges/commit`

### Return Values

Parameter | Type | Description
--------- | ---- | ---------
charge | Object | The charge object generated from the provided details.


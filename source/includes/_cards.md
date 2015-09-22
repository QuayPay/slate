# Cards

## Get All Cards

```javascript
qp.getCards().then(function(response) { console.log(response.data) });
```
```json
{
  "total": 2,
  "results": [
    {
      "id": "72da85b5fd46a356aa356b7d30cd88660bf",
      "brand": "visa",
      "last_four": "4242"
    },
    {
      "id": "216baeb5fd46a356ae9f30cd8454f0bf4e1",
      "brand": "visa",
      "last_four": "8630"
    }
  ]
}
```

Retrieves all cards associated with the authenticated account.

### HTTP Request

`GET https://gateway.quaypay.com/api/v2/cards`

### Return Values

Parameter | Type | Description
--------- | ------- | -----------
total | Number | The number of records returned.
results | Array | An array of cards owned by the user.

<aside class="notice">
A merchant does not have the ability to retreive cards belonging to other users.
</aside>

## Get a Specific Card

```javascript
qp.getCard('72da85b5fd46a356aa356b7d30cd88660bf').then(function(response) { console.log(response.data) });
```

```json
{
  "card": {
    "id": "72da85b5fd46a356aa356b7d30cd88660bf",
    "brand": "visa",
    "last_four": "4242"
  }
}
```


Retrieve a specific card.


### HTTP Request

`GET https://gateway.quaypay.com/api/v2/cards/:id`

### Return Values

Parameter | Type | Description
--------- | ---- | ---------
card | Object | The card associated with the ID passed in.


## Add a Card

```javascript
qp.addCard({ 
    name: 'Bob Smith',
    number: '4242 4242 4242 4242',
    exp_month: '6',
    exp_year: '2016',
    cvc: '100'
  }).then(function(response) { console.log(response.data) });
```
```json
{
  "card": {
    "id": "72da85b5fd46a356aa356b7d30cd88660bf",
    "brand": "visa",
    "last_four": "4242"
  }
}
```

Add a card to the currently authenticated account. 

A successful response returns the details of the card, including the ID which can be used to make payments straight away.


### HTTP Request

`POST https://gateway.quaypay.com/api/v2/cards`

### Return Values

Parameter | Type | Description
--------- | ---- | ---------
card | Object | The card object generated from the provided details.
## Delete a Card

```javascript
qp.deleteCard('72da85b5fd46a356aa356b7d30cd88660bf').then(function(response) { console.log(response.status) });

> 200
```


Delete a specific card.

Returns status code `200` when a card is deleted successfully.


### HTTP Request

`DELETE https://gateway.quaypay.com/api/v2/cards/:id`


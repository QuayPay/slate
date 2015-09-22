# Applications

An application object holds configuration and authentication settings defining how the QuayPay API will be used. 

After signing up for developer access, you are provided with an application ID used to retreive and set these attributes.

### Attributes

Attribute | Type | Description
--------- | ------- | -----------
id |String| 
auth_method | String | The method of displaying the login page to the end user.
auth_providers | Array | The authentication providers allowed for users to authenticate against the application.
live | Boolean | Whether the gateway is currently accepting live or test payments.
points | Object | Defines the configuration of <a href="#points">loyalty points</a>.
redirect_uri |String| Where to redirect users after successfully authenticating via login providers. 
secret |String| Used to commit requests and authenticate without oAuth.

## Retreiving an Application

```javascript
qp.getApplication().then(function(response) { console.log(response.data) });
```
```json
{
	"id": "testappid",
	"auth_method": "iframe",
	"auth_providers": "['facebook, google, form']",
	"live": false,
	"points": {
		"exchange": 0.2,
		"buy_rules": [
			{
				"range": [0, 500],
				"points": 0,
				"percent": 0.5
			},
			{
				"range": [500, 2000],
				"points": 500,
				"percent": 0
			}

		]
	},
	"redirect_uri": "http://merchant.com/logins/oauth.html"
}
```

```shell
curl https://gateway.quaypay.com/api/v2/applications/testappid \
    -H "Authorization: Bearer f3ab55c097727130fdc183529131fadd4b36b7ec23fc968a7d776e56468f7134"

> { 
	application: {
    	id: testappid,
    	auth_method: 'iframe',
    	auth_providers: ['facebook, google, form'],
    	live: false,
    	points: {
			exchange: 0.2,
			buy_rules: [
				{
					range: [0, 500],
					points: 0,
					percent: 0.5
				},
				{
					range: [500, 2000],
					points: 500,
					percent: 0
				}

			]
		},
		redirect_uri: 'http://merchant.com/logins/oauth.html'
	}
}
```

The data returned when retreiving an application is dependent on your level of <a href="#authentication">authentication</a> when making the request.

When unathenticated or using a non-merchant account to generate your API token, only the `auth_method`, `auth_providers` and `redirect_uri` are returned. 

When using a merchant account to generate your API token, all fields except the application secret are returned.


## Modifying an Application

```javascript
qp.updateApplication({auth_method: 'popup'});

> {
	id: testappid,
	auth_method: 'popup',
	...
}

```

```shell
curl https://gateway.quaypay.com/api/v2/applications/testappid \
    -X PUT \
    -H 'Content-Type: application/json' \ 
    -H "Authorization: Bearer f3ab55c097727130fdc183529131fadd4b36b7ec23fc968a7d776e56468f7134" \
    -d '{ "application": { "auth_method": "popup" } }'

> { 
	application: {
    	id: testappid,
    	auth_method: 'popup',
    	...
    }
}
```


To update your application, pass in an object containing the attrivutes you wish to update and their new values. 

The updated application is returned after a successful request is made.
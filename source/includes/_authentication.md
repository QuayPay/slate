# Authentication

## Obtaining an Authorization Token

```shell
curl -F response_type=code \
	-F client_id= "< CLIENT_ID >" \
	-F client_secret= "< CLIENT_SECRET >"  \
	-F redirect_uri=urn:ietf:wg:oauth:2.0:oob \
	-F username=user@example.com \
	-X POST http://localhost:3000/oauth/authorize
```
```javascript
qp.init({
	clientId:"< CLIENT_ID >",
	redirect:"< REDIRECT_URI >",
	loginProviders: [ "< PROVIDER >", "< PROVIDER >"]
});
```
QuayPay uses the oAuth2 framework to authorise requests.

Clients must pass the following fields to QuayPay's servers during the authentication process:

Parameter | Default | Description
--------- | ------- | -----------
Client ID | N/A | Provided by QuayPay and used to authenticate on the client side.
Client Secret | N/A | Provided by QuayPay and used to authenticate on the server side.
Redirect URI | N/A | Where to redirect users after successfully authenticating via login providers.
Login Providers | ['google', 'facebook', 'form'] | The authentication providers allowed for users to authenticate against the application.
Login Method | 'iframe' | The method of displaying the login page to the end user.

> Make sure to replace `< FIELD >` with the authentication data provided by QuayPay.


Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`


<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>


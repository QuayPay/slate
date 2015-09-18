# Applications

An application object holds configuration and authentication settings defining how the QuayPay API will be used. 

After signing up for developer access, you are provided with an application ID used to retreive and set these attributes.

### Attributes for Authentication

Attribute | Default | Description
--------- | ------- | -----------
id | N/A | 
secret | N/A | 
redirect_uri | N/A | Where to redirect users after successfully authenticating via login providers.
auth_providers | ['google', 'facebook', 'form'] | The authentication providers allowed for users to authenticate against the application. 
auth_method | 'iframe' | The method of displaying the login page to the end user.

### Attributes for Gateway Settings

Attribute | Default | Description
--------- | ------- | -----------
live | false | Whether the gateway is currently accepting live or test payments.


### Attributes for Loyalty Points Settings
Attribute | Default | Description
--------- | ------- | -----------
live | false | Whether the gateway is currently accepting live or test payments.

> Make sure to replace `< FIELD >` with the authentication data provided by QuayPay.


Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`


<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>


# Authentication

## Using the Client Library

```javascript
qp.init({
	client_id:"testappid",
	redirect_uri:"http://merchant.com/auth/post_token.html",
	auth_providers: [ "facebook", "form" ]
});
```

Using our JavaScript client library makes authentication very easy, requiring only three parameters:

- `client_id` is your application's ID provided for you after signup
- `redirect_uri` is where QuayPay will redirect to with an access token upon successful authentication
- `auth_providers` is either the set or a subset of the available methods for authentication

For the example on the right, when a user attempts to make any unauthorized API request, they are prompted to login to QuayPay via either Facebook or a form based login.

The method used to direct a user to the prompt to login is defined by the application's `auth_method` attribute. This is set to `'iframe'` by default but can hold the values `'popup'` for a popup window or `'redirect'` for a full page redirect to the login prompt.

Once successfully authenticated, the `auth_method` used to display the authentication options is redirected to the `redirect_uri` with an access token as a url parameter. This access token is then passed back to the client library using postMessage and stored in the browser's localStorage for future requests.

## Auth Providers

Merchants have the ability to decide how users authenticate themselves against the QuayPay API. The provideres of this authentication fit into three categories:

### QuayPay Form

The classic form registration and login is the default provider for API authentication. By default, these forms are shown in an overlayed iframe allowing the customer to enter their email and password to authenticate.

### Third Party Federated Identity

Merchants may allow customers to register and login using third party federated identity providers, generally provided by social networking services such as Facebook or Google. When a user has an existing session with one of these providers, registration and login are generally single-click actions.

QuayPay currently provides access to the authentication services of Facebook and Google but merchants may request support for other providers.

### Merchant Federated Identity

Merchants who wish to have users authenticated on QuayPay using their own website's authentication scheme must support the oAuth2 standard for delegation of access to user resources by QuayPay.


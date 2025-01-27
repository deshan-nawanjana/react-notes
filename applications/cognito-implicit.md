# Cognito Implicit Flow

Cognito Hosted UI is a `separated module` in AWS that you can use to authenticate your application.

Therefore, while using Cognito, you are `not required` to create a login interface in your web application. Only thing you need to do is to redirect to the Cognito login page. Then you will have an interface to enter your login details or create an account. Once you have successfully logged in, it will redirect back to your application with access token.

## Login with Cognito

Look at the following Cognito login example URL

```
https://sample-user-pool.auth.sample-region.amazoncognito.com/login?client_id=sample-client-id&response_type=token&scope=email+openid+profile&redirect_uri=http://localhost:3000/
```

This URL contains following specific options.

- `user_pool` - Identifier of users collection defined in AWS
- `aws_region` - AWS region
- `client_id` - Identifier of login client
- `response_type` - How should you receive the authentication data
- `scope` - Which info are you requesting from user
- `redirect_uri` - Where to redirect after successfully logged in

Therefore, we have the standard format of Cognito login URL as follows

```
https://[user_pool].auth.[aws_region].amazoncognito.com/login
  ?client_id=[client_id]
  &response_type=[response_type]
  &scope=[scope]
  &redirect_uri=[redirect_uri]
```

Once the user has successfully logged in, it will redirect to the given `redirect_uri` in the options with `id_token` and `access_token` included in the url hash.

```
http://localhost:3000/#id_token=eyJraWQiOi....&access_token=eyJraW....
```

Using any method in your application, you can read those tokens as use for the server communication.

## Get User Info

While you have the Cognito `access_token` from the authentication, you can use it to call the following `GET` API to receive user info data object.

Make sure to send the `access_token` with the `Authorization` header.

Send the same `user_pool` and `aws_region` used in the login URL.

- Request method - `GET`
- Headers
  - Authorization: "Bearer [access_token]"

```
https://[user_pool].auth.[aws_region].amazoncognito.com/oauth2/userInfo
```

# Enable Authentication for OAuth/OpenID Connect Web Application

This page guides you through enabling authentication to an OAuth/OpenID Connect web application. 

---

This guide assumes you have your own application. If you wish to try out this flow with a sample application, click the button below. 

<a class="samplebtn_a" href="../../samples/regular-webapp-oidc-sample" target="_blank" rel="nofollow noopener">Try it with the sample</a>

----

{!authenticate/register-an-sp.md!}

----

{!authenticate/oauth-app-config-basic.md!}

----

## Configure the client application

Make the following requests via your application to connect your application to WSO2 IS. 

1. Obtain the `authorization_code` by sending an authorization request to the authorization endpoint.

    !!! tip
        If you have made PKCE mandatory, include the `code_challenge` and `code_challenge_method` parameters in the request. You can use [an online tool](https://tonyxu-io.github.io/pkce-generator/) to generate PKCE code challenges.

    ```tab="Request Format"
    https://<host>/oauth2/authorize?scope=openid&response_type=code
    &redirect_uri=<redirect_uri>
    &client_id=<client_id>
    &code_challenge=<PKCE_code_challenge>
    &code_challenge_method=<PKCE_code_challenge_method>
    ```

    ```tab="Sample Request"
    https://localhost:9443/oauth2/authorize?scope=openid&response_type=code
    &redirect_uri=https://localhost/callback
    &client_id=YYVdAL3lLcmrubZ2IkflCAuLwk0a
    &code_challenge=5vEtIy2T-G65yXHc8g5zcJDQXICBzZMrtERq0zhx7hM
    &code_challenge_method=S256
    ```

2. Obtain the access token by sending a token request to the token endpoint using the `authorization_code` recieved in step 1, and the `Client_ID` and `<Client_Secret>` obtained when configuring the service provider.

    !!! tip
        If you are using PKCE, include the `code_verifier` parameter in the request.

    ```tab="Request Format"
    curl -i -X POST -u <Client_ID>:<Client_Secret> -k -d 
    'grant_type=authorization_code&redirect_uri=<redirect_uri>
    &code=<authorization_code>&code_verifier=<PKCE_code_verifier>' 
    https://localhost:9443/oauth2/token
    ```

    ```tab="Sample Request"
    curl -i -X POST -u YYVdAL3lLcmrubZ2IkflCAuLwk0a:azd39swy3Krt59fLjewYuD_EylIa -k -d 
    'grant_type=authorization_code
    &redirect_uri=https://localhost/callback&code=d827ec7e-1b8e-3d81-a4c0-2f7ff67ce844
    &code_verifier=aYr1jbrAHhZDC5WBi8wQPdraATAvvKy93S22rkPDkkRTHzzaAMVOJ5MHgRPgoKf8xDBJPE08'
    https://localhost:9443/oauth2/token
    ```

3. Validate the ID token. For the token request, you will receive a response containing the access token, scope, and ID token. The ID token contains basic user information. To check what is encoded within the ID token, you can use a tool such as <jwt.io>.

----



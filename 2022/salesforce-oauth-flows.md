# Salesforce Oauth Authorization Flows

A `flow` is a sequence of network requests for an app to get an access token. An `access token` allows an app to talk to a server on behalf of the user.

An app that talks to Salesforce is called a `Connected App`. It needs to be registered through Setup which will generate `consumer key` and a `consumer secret`. The key is referred to as an `initial access token`. The secret is private and should only be used in environments where the app is hosted in a secure environment - never on a client's computer. See [Connected App Configuration](2022/salesforce-connected-app-config.md).

There are several [authentication flows for Salesforce](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5). This is a gist of the documentation.

For the oauth2 flows, you use one or both of the following endpoints:

-   **Authorize endpoint**: `https://login.salesforce.com//services/oauth2/authorize/?...`
-   **Token endpoint**: `https://login.salesforce.com/services/oauth2/token`

Once you receive an `access_token`, you can specify it in the `Authorization` HTTP header for subsequent requests using the `Bearer <access token>` syntax.

## 1. Username-Password Flow

-   Not recommended
-   Can be blocked at org level
-   In the POST request to the token endpoint, specify
    -   as `grant_type`, the text `password`
    -   as `client_id`, the "consumer key"
    -   as `client_secret`, the "consumer secret"
    -   as `username`, the name of the user
    -   as `password`, the user's password
-   Receive an `asset_token` that you can use in the `Authorization` HTTP Header.

## 2. Web Server Flow

-   Used when the app is hosted on a secure server, and has access to client secret.
-   In the initial GET request to the authorize endpoint, specify
    -   as `response type`, the text `code`
    -   as `client_id`, the "consumer key"
    -   as `redirect_uri`, the path the the local web server that handles auth
-   In the subsequent POST request to the token endpoint, specify
    -   as `grant_type` the text `authorization_code`
    -   as `code` the value you received from the initial GET
    -   as `client_id`, the "consumer key"
    -   as `client_secret`, the "consumer secret" (if "Require Secret for Web Server Flow" is checked in the Connected App settings)
    -   as `redirect_uri`, the path the the local web server that handles the auth

## 3. User-Agent Flow

-   Has the advantage of not requiring client secret
-   In the GET request to the authorize endpoint, specify
    -   as `response_type`, the text `token`
    -   as `client_id`, the "consumer key"
    -   as `redirect_uri`, the path the the local web server that handles auth
-   Receive a GET request at the redirect URI where the hash contains the key-value pairs

    Example Outgoing Request:

    ```
    https://login.salesforce.com/services/oauth2/authorize?response_type=token&client_id=CONSUMER-KEY&redirect_uri=http://localhost:8000
    ```

    Example Incoming Request:

    ```
    http://localhost:8000/#access_token=SOME-ID&refresh_token=SOME-OTHER-ID&instance_url=https%3A%2F%2Fresourceful-seal-dev-ed.my.salesforce.com&id=https%3A%2F%2Flogin.salesforce.com%2Fid%2FSOME-ORG-ID%2FSOME-USER-ID&issued_at=SOME-NUMBER&signature=SOME-SIGNATURE%3D&scope=id+api+full+refresh_token&token_type=Bearer
    ```

    Because the server code can't read hashes (`req.url.hash` will be empty), we need a little bit of client-code that parses the hash and relays it to another endpoint as part of the URL path (not hash). See [this for an example](https://github.com/Levent0z/node-cli-oauth2/blob/main/login-result.html).

-   No subsequent POST needed.

## 4. Device Flow

-   For use in IoT devices "with limited input or display capabilitied" and command-line (CLI) applications
-   In the initial POST request to the token endpoint, specify
    -   as `response type`, the text `device_code`
    -   as `client_id`, the "consumer key"
-   Receive
    -   as `device_code`, a long code (valid for 10 minutes)
    -   as `user_code`, an 8-char code (valid for 10 minutes)
    -   as `verification_uri`, a URL for the user to enter the user code
    -   as `interval`, minimum polling duration
-   Instruct user to enter `user_code` at `verification_uri`
-   Poll the token endpoint until successful (or timeout). Specify
    -   as `grant_type`, the text `device`
    -   as `client_id`, the "consumer key"
    -   as `code` the `device_code` you received from the initial POST

## 5. Refresh Token Flow

-   A refresh token allows an app to request a new access token using a previously granted refresh token. [Why use a refresh token](https://stackoverflow.com/questions/38986005/what-is-the-purpose-of-a-refresh-token)
-   In the POST request, specify
    -   as `grant_type`, the text `refresh_token`
    -   as `client_id`, the "consumer key"
    -   as `client_secret`, the "consumer secret" but only if "Require Secret for Refresh Token Flow" is checked in the Connected App settings
    -   as `refresh_token` the value you received for it in the initial access grant.

## 6. Asset Token Flow

-   For use in integrating IoT devices
-   Uses JWT
-   [Demo](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_asset_token_explorer_demo_app.htm&type=5)

## 7. SAML Bearer Assertion Flow

-   Client provides a signed SAML asswertion

## References

-   [OAuth Authorization Flows](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)
-   [Oauth Authorization flows in Salesforce | Web Server flow | JWT Bearer token flow](https://www.youtube.com/watch?v=cViU2-xVscA)
-   [Browser SSO for CLI Applications](https://hasinthaindrajee.medium.com/browser-sso-for-cli-applications-b0be743fa656)

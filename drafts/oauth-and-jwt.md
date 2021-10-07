# OAUTH & JWT

## Create a private key & self-signed certificate

[Detailed Docs](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_auth_key_and_cert.htm)

Replace `PASSWORD` below:

```sh
mkdir ~/TMP
cd ~/TMP
openssl genrsa -des3 -passout pass:PASSWORD -out server.pass.key 2048
openssl rsa -passin pass:PASSWORD -in server.pass.key -out server.key
rm server.pass.key # No longer needed
openssl req -new -key server.key -out server.csr # New certificate request
openssl x509 -req -sha256 -days 365 -in server.csr -signkey server.key -out server.crt # Self-sign
cat server.key | pbcopy # Copy private key to the clipboard to be used in server-side configurations
```

This will result in the following files to be created:

- server.key
- server.csr
- server.crt

## Adding certificate to a Salesforce Org

1. Login to org and got to Setup
2. Apps --> App Manager
3. Select your Connected App, click `Edit` in the drop down at the last column
4. Check `Use digital signatures`
5. Upload your `.crt` file.

## NPM Package for JWT Bearer Token Flow

[Salesforce OAuth 2.0 JWT Bearer Token Flow](https://www.npmjs.com/package/salesforce-jwt-bearer-token-flow)

## SSO for a Heroku app using Salesforce as Identity Provider

[Video - SSO via SAML](https://salesforce.vidyard.com/watch/izBK7xFMWhqJXsLuqD8kAJ)

## Axiom SSO Tools

Axiom is a web-based suite of tools for learning, testing, and troubleshooting single sign-on solutions for Salesforce.com, available at https://axiomsso.herokuapp.com. The tools include:

- SAML Identity Provider & Tester
- Token-Based Authentication
- Self Authentication Service
- OAuth Tester

[Source on GitHub](https://github.com/ryanbrainard/axiom)

To be able to run the Oath2 scenario in Axiom, in Setup:

- Create a Connected App & enable OAuth
- Add the ip address of https://axiomsso.herokuapp.com (54.208.186.182) to `Security > Network Access` in Setup.

Once connected you get an ID and an access token. Example:

- Id: https://login.salesforce.com/id/18CHARORGID/18CHARUSERID
- Access Token: 15CHARORGID!GOBBLEDYGOOK

You can use it with identity as follows
https://login.salesforce.com/id/18CHARORGID/18CHARUSERID?oauth_token=15CHARORGID!GOBBLEDYGOOK


---

## Using SOAP

POST to https://login.salesforce.com/services/Soap/c/v29.0

### HTTP Request

#### Headers

Default "Postman" headers + 
- `SOAPAction: "urn:enterprise.soap.sforce.com/login"`
- `Content-Type: text/xml`

#### Body

As "raw", replace uppercase values:

```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"
                xmlns:tns="urn:enterprise.soap.sforce.com"
                xmlns:fns="urn:fault.enterprise.soap.sforce.com"
                xmlns:ens="urn:sobject.enterprise.soap.sforce.com">
    <soap:Header>
    </soap:Header>
    <soap:Body>
        <tns:login>
            <username>USERNAME@DOMAIN</username>
            <password>PASSWORD</password>
        </tns:login>
    </soap:Body>
</soap:Envelope>
```

### HTTP Response

Note: Uppercase text are substitutions for redacted values.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:enterprise.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Body>
        <loginResponse>
            <result>
                <passwordExpired>false</passwordExpired>
                <serverUrl>https://HOSTNAME.my.salesforce.com/services/Soap/c/7.0/ORGID</serverUrl>
                <sessionId>ORGID!GOBBLEDYGOOK</sessionId>
                <userId>USERID</userId>
                <userInfo>
                    <accessibilityMode>false</accessibilityMode>
                    <currencySymbol>$</currencySymbol>
                    <organizationId>ORGID</organizationId>
                    <organizationMultiCurrency>false</organizationMultiCurrency>
                    <organizationName>Salesforce</organizationName>
                    <userDefaultCurrencyIsoCode xsi:nil="true"/>
                    <userEmail>EMAIL</userEmail>
                    <userFullName>FIRST LASTz</userFullName>
                    <userId>USERID</userId>
                    <userLanguage>en_US</userLanguage>
                    <userLocale>en_US</userLocale>
                    <userTimeZone>America/Los_Angeles</userTimeZone>
                    <userUiSkin>Theme3</userUiSkin>
                </userInfo>
            </result>
        </loginResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
You can then extract the sessionId and use it as a bearer token in subsequent requests:
Example:

`Authorization: Bearer ORGID!GOBBLEDYGOOK`




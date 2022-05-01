# Web Security Concepts

## XSS 

"Cross-Site Scripting"

It's an injection attack. 

- **How it works**: Hacker puts in code/script into a user input, the script gets run on the browser when reflected or viewed later.
- **Solution**: Validate and encode user input before reflecting/storing.

3 orginal types (that can overlap):
1.  `DOM-Based XSS`: When the entire data flow never leaves the brower.
2.  `Reflected/Non-Persistent XSS`: Malicious input is immediately returned to the user as an error message, search result.
3.  `Stored/Persistent XSS`: Malicious input is stored on a target server/db. The victim retrieves it later. (Note: It can also be stored in the browser.)

2 types as part of new classification:
1. `Server XSS` - User-provided data is included in the HTTP response, where the source could be the request or storage.
2. `Client XSS` - User-provided data is used to update the DOM with an "unsafe" JavaScript call. "Unsafe" mans JavaScript can be introduced into the DOM.

**Defense**: Context-sensitive server-side output encoding

### Safe Sinks (Sink = where variables are placed into the webpage)
- `.textContent` setter will automatically HTML Entity Encode. `&`, `<`, `>`, `"`, `'`. Prefer this instead of the unseafe `innerHTML`.
- `.setAttribute()` method will automatically HTML Attribute Encode.
- `style.property` setter will automatically CSS Encode.
- `encodeURIComponent()` method will automaticaly URL encode.

[More on owasp.org](https://owasp.org/www-community/attacks/xss/)

## CSRF / XSRF

"Cross-Site Request Forgery"

It's an attack that might require "social engineering".

- **How it works**: Hacker forces a valid user to click on a link to the resource (e.g. bank), which uses the user's established session token to do its bidding.
- **Idea**: Check `Referer` header, but may not always be sent due to privacy
- **Solution 1**: A one time key called a `nonce`. Server can create a random value sent with the form (in a hidden input field) and is expected to be sent back. This is called the [Synchronizer Token Pattern](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern)
- **Solution 2**: [Double Submit Cookie](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#double-submit-cookie) method is stateless. Send a random value both in a cookie and a request parameter. Every request is required to include the value in the form. If the value in the cookie and the hidden input field match, it's legitimate.

A hacker can hide `GET` URLs in `<a>` and `<img>` tags and `POST` URLs in a `<form>` tag. In the POST case, the submission of the form can be done via JavaScript too. In the case of `PUT`, a `<script>` tag can be used (in an exploit page) to send a request, but will be blocked by `CORS` if setup correctly.

[More on owasp.org](https://owasp.org/www-community/attacks/csrf/)


## CORS
"Cross-Origin Resource Sharing"

- Server adds `Access-Control-Allow-Origin` header to the response. If set to `*`, all is alloed. The client (browser) is responsible for allowing/denying a request.
- Note: Client can change/override `Origin` header value.

["Simple requests"](https://developer.mozilla.org/en-US/docs/web/http/cors#simple_requests) don't trigger a `CORS preflight`:
- They are one of `GET`, `HEAD` or `POST`.
- Only CORS-safelisted headers are allowed, e.g. `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, `Range`.
- If `Content-Type` is used, only the following are allowed:
  - `application/x-www-form-urlencoded`
  - `multipart/form-data`
  - `text/plain`
- ... there are others

## Cookie Attributes

`HttpOnly`: Not available to scripting
`SameSite`: Lax (default), Strict or None. 

## Security around Caching

### Prevent Caching Pages
```html
<meta name="robots" content="noindex,nofollow">
```

### HTTPS responses are cachable by default
- Don't return sensitive data in HTTPS responses (e.g. input value for type=password)
- Implement anti-caching headers:  `Cache-control: no-store` or `Pragma: no-cache` headers

### Prevent caching input values
- Use `autocomplete="off"` for `<input>` elements with sensitive data

### Prevent caching in server logs and client history
- Use `POST` instead of `GET`


## COOP
"Cross-Origin Opener Policy"

The `Cross-Origin-Opener-Policy` HTTP response header allows you to ensure a top-level document does not share a browsing context group with cross-origin documents.

COOP will process-isolate your document and potential attackers can't access your global object if they were to open it in a popup, preventing a set of cross-origin attacks dubbed XS-Leaks.


## CORP
"Cross-Origin Resource Policy"

- Allows you to control the set of origins that are empowered to include a resource.
- The policy is only effective for no-cors requests, which are issued by default for CORS-safelisted methods/headers.

- [More on Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cross-Origin_Resource_Policy_(CORP))
- [More on Resource Policies](https://resourcepolicy.fyi/)

## CSP
"Content Security Policy"

- Control resources the user agent is allowed to load for a given page. 
- With a few exceptions, policies mostly involve specifying server origins and script endpoints. 
- Helps guard against cross-site scripting attacks 

Policy-directives are directives paired with values when configuring CSP in the `Content-Security-Policy` header. For example:

```
Content-Security-Policy: <policy-directive>; <policy-directive>
Content-Security-Policy: <directive> <source>;
Content-Security-Policy: <directive> <source> <source>;
```

- [More on Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)

### Directives

[Fetch directives](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy#fetch_directives) control the locations from which certain resource types may be loaded.

| type      | directive         | controls                                      |
| --------- | ----------------- | --------------------------------------------- |
| fetch     | `child-src`       | web workers, `<frame>`, `<iframe>`            |
| fetch     | `default-src`     | (fallback value)                              |
| fetch     | `font-src`        | `@font-face`                                  |
| fetch     | `frame-src`       | `<frame>`, `<iframe>`                         |
| fetch     | `img-src`         | `<img>` and favicons                          |
| fetch     | `manifest-src`    | application manifest files                    |
| fetch     | `media-src`       | `<audio>`, `<video>`, `<track>`               |
| fetch     | `object-src`      | `<object>`, `<embed>`, `<applet>`             |
| fetch     | `script-src`      | `<script>`                                    |
| fetch     | `style-src`       | stylesheets                                   |
| nav       | `form-action`     | submision for a form                          |
| nav       | `frame-ancestors` | specified valid parents that may embed a page |
| reporting | `report-uri`      | CSP violations endpoint                       |

### Values

| value           | description                                                                                             |
| --------------- | ------------------------------------------------------------------------------------------------------- |
| `none`          | Don't allow loading of any resources                                                                    |
| `self`          | Only allow from current origin                                                                          |
| `unsafe-inline` | Allow use of inline resources.                                                                          |
| `unsafe-eval`   | Allow use of `eval`                                                                                     |
| Host value      | example.com, *.example.com, example.com/path_ending_with_slash/, https://example.com/exact/path.js, ... |
| Scheme value    | https:, data:, ...                                                                                      |
| nonce-*         | nonce-someguidsomeguidsomeguid                                                                          |
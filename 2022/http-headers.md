# HTTP Headers

- `End-to-end` headers: headers must be transmitted to the final recipient (proxies must retransmit, caches must store)
- `Hop-by-hop` headers: Meaningful only for a single transport-level connection. (must not be retransmitted or cached)

| category | header                              | description                                                                                                |
| -------- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Auth.    | `Authorization`                     | auth-scheme csv-authorization-parameters                                                                   |
| Cache    | `Age`                               | value-in-seconds                                                                                           |
| Cache    | `Cache-Control`                     | Example directives: `max-age`, `no-cache`, `no-store`, `stale-if-error`                                    |
| Cache    | `Clear-Site-Data`                   | Clears cookies, storage, cache associated with the server                                                  |
| Cache    | `Expires`                           | An HTTP Date/time after which response will be stale. Ignored if `Cache-Control` with `max-age` is present |
| Cache    | `Pragma`                            | Used for HTTP/1.0 caches where Cache-Control is absent.                                                    |
| Cond.    | `Last-Modified`                     |                                                                                                            |
| Cond.    | `ETag`                              | A unique string identifying the version of the resource. Used by conditional headers.                      |
| Cond.    | `If-Match`                          |                                                                                                            |
| Cond.    | `If-None-Match`                     |                                                                                                            |
| Cond.    | `If-Modified-Since`                 |                                                                                                            |
| Cond.    | `Vary`                              |                                                                                                            |
| Conn.    | `Connection`                        | Controls whether the network connection stays open                                                         |
| Conn.    | `Keep-Alive`                        | Controls how long persistent connection stays open                                                         |
| Content  | `Accept`                            | Accepted types of data                                                                                     |
| Content  | `Accept-Encoding`                   | Accepted compression algorithms                                                                            |
| Content  | `Accept-Language`                   | Hint expected human language for server responses                                                          |
| Content  | `Content-Length`                    | Size of resources in decimal number of bytes                                                               |
| Content  | `Content-Type`                      | Indicates the type of the sources                                                                          |
| Content  | `Content-Encoding`                  | Specified the compression algorithm                                                                        |
| Content  | `Content-Language`                  | The human language intended for the audience                                                               |
| Content  | `Content-Location`                  | Indicates alternate location for the returned data                                                         |
| Control  | `Expect`                            | Expectations of the server                                                                                 |
| Cookies  | `Cookie`                            | Stored HTTP cookies                                                                                        |
| Cookies  | `Set-Cookie`                        | Send cookies from the server to the user-agent                                                             |
| CORS     | `Access-Control-Allow-Origin`       | Indicates whether the response can be shared.                                                              |
| CORS     | `Access-Control-Allow-Credentials`  | Indicates whether the response can be exposed when the credentials flag is true.                           |
| CORS     | `Access-Control-Allow-Headers`      | In response to a preflight request, lists allowed HTTP headers                                             |
| CORS     | `Access-Control-Allow-Methods`      | In response to a preflight request, lists allowed HTTP methods                                             |
| CORS     | `Access-Control-Expose-Headers`     | List of headers that can be exposed                                                                        |
| CORS     | `Access-Control-Max-Age`            | Preflight request cache time                                                                               |
| CORS     | `Access-Control-Request-Headers`    | During preflight, specify HTTP headers that will be used in the actual request                             |
| CORS     | `Access-Control-Request-Method`     | During preflight, specify which HTTP method will be used                                                   |
| CORS     | `Origin`                            | Where a fetch originates from                                                                              |
| CORS     | `Timing-Allow-Origin`               | Origins that are allowed to see values from Resource Timing API                                            |
| Download | `Content-Disposition`               | Whether to display a downloaded file inline or pop up a "Save As" dialog                                   |
| Proxy    | `Forwarded`                         | Optionally added by reverse proxy servers that would otherwise be altered or lost due to proxying          |
| Proxy    | `Via`                               |                                                                                                            |
| Redirect | `Location`                          | The URL to redirect a page to.                                                                             |
| Request  | `From`                              |                                                                                                            |
| Request  | `Host`                              | Domain name of the server (for virtual hosting), and (optionally) the TCP port number                      |
| Request  | `Referer`                           | The address of the previous web page from which a link to the currently requested page was followed.       |
| Request  | `Referrer-Policy`                   | Which referrer information sent in the Referer header should be included with requests made                |
| Request  | `User-Agent`                        | Identifies application type, operating system, software vendor or software version of the client           |
| Response | `Allow`                             | HTTP request methods supported by a resource.                                                              |
| Response | `Server`                            | Information about the software used by the origin server to handle the request                             |
| Range    | ...                                 |                                                                                                            |
| Security | `Cross-Origin-Embedder-Policy`      | Prevents loading any cross-origin resources that don't explicitly grant the document permission            |
| Security | `Cross-Origin-Opener-Policy`        | Allows to block a top-level document from sharing a browsing context group with cross-origin docs          |
| Security | `Cross-Origin-Resource-Policy`      | Browser should block no-cors cross-origin/cross-site requests to the given resource                        |
| Security | `Cross-Security-Policy`             | Controls resources the user agent is allowed to load for a given page.                                     |
| Security | `Cross-Security-Policy-Report-Only` | Allows experimentation without enforcing. JSON Reports are sent via POST to the specified URI              |

Also check out [Web Security](web-security.md) for more details.

## Example Values

| header                             | Examples                                                                        |
| ---------------------------------- | ------------------------------------------------------------------------------- |
| `Authorization`                    | Basic credentials                                                               |
| `Age`                              | 60                                                                              |
| `Cache-Control`                    | max-age=604800                                                                  |
| `Expires`                          | Wed, 21 Oct 2015 07:28:00 GMT                                                   |
| `Connection`                       | `close` (default), `keep-alive`                                                 |
| `Keep-Alive`                       | `timeout`=5, `max`=1000                                                         |
| `Accept`                           | application/json, text/json, application/xml, text/plain, text/markdown, text/* |
| `Content-Type`                     | multipart/form-data; boundary=something                                         |
| `Content-Language`                 | en-US, en-CA, de-DE                                                             |
| `Cookie`                           | name=value; name2=value2; ...                                                   |
| `Set-Cookie`                       | name=value; booleanProperty; property=value; ...                                |
| `Access-Control-Allow-Origin`      | `*`,  origin                                                                    |
| `Access-Control-Allow-Credentials` | `true` (note: false is not valid, just omit the header)                         |
| `Access-Control-Request-Method`    | OPTIONS, GET, POST, DELETE, ...                                                 |
| `Referrer-Policy`                  | `no-referrer`, `strict-origin-when-cross-origin` (default), ...                 |
| `Cross-Origin-Embedder-Policy`     | `unsafe-none` (default) \| `require-corp`                                       |
| `Cross-Origin-Opener-Policy`       | `unsafe-none` (default) \| `same-origin-allow-popups` \| `same-origin`          |
| `Cross-Origin-Resource-Policy`     | `same-origin` \| `same-site` \| `cross-origin` (default)                        |

[More on Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
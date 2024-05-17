---
tags:
  - note
---
# `= this.file.name`
---

The following table lists application settings.

Note that sub-apps will:

- Not inherit the value of settings that have a default value. You must set the value in the sub-app.
- Inherit the value of settings with no default value; these are explicitly noted in the table below.

Exceptions: Sub-apps will inherit the value of `trust proxy` even though it has a default value (for backward-compatibility); Sub-apps will not inherit the value of `view cache` in production (when `NODE_ENV` is “production”).

|Property|Type|Description|Default|
|---|---|---|---|
|`case sensitive routing`|Boolean|Enable case sensitivity. When enabled, "/Foo" and "/foo" are different routes. When disabled, "/Foo" and "/foo" are treated the same.<br><br>**NOTE**: Sub-apps will inherit the value of this setting.|N/A (undefined)|
|`env`|String|Environment mode. Be sure to set to "production" in a production environment; see [Production best practices: performance and reliability](http://expressjs.com/advanced/best-practice-performance.html#env).|`process.env.NODE_ENV` (`NODE_ENV` environment variable) or “development” if `NODE_ENV` is not set.|
|`etag`|Varied|Set the ETag response header. For possible values, see the [`etag` options table](http://expressjs.com/en/4x/api.html#etag.options.table).<br><br>[More about the HTTP ETag header](http://en.wikipedia.org/wiki/HTTP_ETag).|`weak`|
|`jsonp callback name`|String|Specifies the default JSONP callback name.|“callback”|
|`json escape`|Boolean|Enable escaping JSON responses from the `res.json`, `res.jsonp`, and `res.send` APIs. This will escape the characters `<`, `>`, and `&` as Unicode escape sequences in JSON. The purpose of this it to assist with [mitigating certain types of persistent XSS attacks](https://blog.mozilla.org/security/2017/07/18/web-service-audits-firefox-accounts/) when clients sniff responses for HTML.<br><br>**NOTE**: Sub-apps will inherit the value of this setting.|N/A (undefined)|
|`json replacer`|Varied|The ['replacer' argument used by `JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#The_replacer_parameter).<br><br>**NOTE**: Sub-apps will inherit the value of this setting.|N/A (undefined)|
|`json spaces`|Varied|The ['space' argument used by `JSON.stringify`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#The_space_argument). This is typically set to the number of spaces to use to indent prettified JSON.<br><br>**NOTE**: Sub-apps will inherit the value of this setting.|N/A (undefined)|
|`query parser`|Varied|Disable query parsing by setting the value to `false`, or set the query parser to use either “simple” or “extended” or a custom query string parsing function.<br><br>The simple query parser is based on Node’s native query parser, [querystring](http://nodejs.org/api/querystring.html).<br><br>The extended query parser is based on [qs](https://www.npmjs.org/package/qs).<br><br>A custom query string parsing function will receive the complete query string, and must return an object of query keys and their values.|"extended"|
|`strict routing`|Boolean|Enable strict routing. When enabled, the router treats "/foo" and "/foo/" as different. Otherwise, the router treats "/foo" and "/foo/" as the same.<br><br>**NOTE**: Sub-apps will inherit the value of this setting.|N/A (undefined)|
|`subdomain offset`|Number|The number of dot-separated parts of the host to remove to access subdomain.|2|
|`trust proxy`|Varied|Indicates the app is behind a front-facing proxy, and to use the `X-Forwarded-*` headers to determine the connection and the IP address of the client. NOTE: `X-Forwarded-*` headers are easily spoofed and the detected IP addresses are unreliable.<br><br>When enabled, Express attempts to determine the IP address of the client connected through the front-facing proxy, or series of proxies. The `req.ips` property, then contains an array of IP addresses the client is connected through. To enable it, use the values described in the [trust proxy options table](http://expressjs.com/en/4x/api.html#trust.proxy.options.table).<br><br>The `trust proxy` setting is implemented using the [proxy-addr](https://www.npmjs.org/package/proxy-addr) package. For more information, see its documentation.<br><br>**NOTE**: Sub-apps _will_ inherit the value of this setting, even though it has a default value.|`false` (disabled)|
|`views`|String or Array|A directory or an array of directories for the application's views. If an array, the views are looked up in the order they occur in the array.|`process.cwd() + '/views'`|
|`view cache`|Boolean|Enables view template compilation caching.<br><br>**NOTE**: Sub-apps will not inherit the value of this setting in production (when `NODE_ENV` is "production").|`true` in production, otherwise undefined.|
|`view engine`|String|The default engine extension to use when omitted.<br><br>**NOTE**: Sub-apps will inherit the value of this setting.|N/A (undefined)|
|`x-powered-by`|Boolean|Enables the "X-Powered-By: Express" HTTP header.|`true`|

---

##### Options for `etag` setting

**NOTE**: These settings apply only to dynamic files, not static files. The [express.static](http://expressjs.com/en/4x/api.html#express.static) middleware ignores these settings.

The ETag functionality is implemented using the [etag](https://www.npmjs.org/package/etag) package. For more information, see its documentation.

|Type|Value|
|---|---|
|Boolean|`true` enables weak ETag. This is the default setting.  <br>`false` disables ETag altogether.|
|String|If "strong", enables strong ETag.  <br>If "weak", enables weak ETag.|
|Function|Custom ETag function implementation. Use this only if you know what you are doing.<br><br>```javascript<br>app.set('etag', function (body, encoding) {<br>  return generateHash(body, encoding) // consider the function is defined<br>})<br>```|

---

##### Options for `trust proxy` setting

Read [Express behind proxies](http://expressjs.com/en/guide/behind-proxies.html) for more information.

|Type|Value|
|---|---|
|Boolean|If `true`, the client’s IP address is understood as the left-most entry in the `X-Forwarded-*` header.<br><br>If `false`, the app is understood as directly facing the Internet and the client’s IP address is derived from `req.connection.remoteAddress`. This is the default setting.|
|String  <br>String containing comma-separated values  <br>Array of strings|An IP address, subnet, or an array of IP addresses, and subnets to trust. Pre-configured subnet names are:<br><br>- loopback - `127.0.0.1/8`, `::1/128`<br>- linklocal - `169.254.0.0/16`, `fe80::/10`<br>- uniquelocal - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `fc00::/7`<br><br>Set IP addresses in any of the following ways:<br><br>Specify a single subnet:<br><br>```javascript<br>app.set('trust proxy', 'loopback')<br>```<br><br>Specify a subnet and an address:<br><br>```javascript<br>app.set('trust proxy', 'loopback, 123.123.123.123')<br>```<br><br>Specify multiple subnets as CSV:<br><br>```javascript<br>app.set('trust proxy', 'loopback, linklocal, uniquelocal')<br>```<br><br>Specify multiple subnets as an array:<br><br>```javascript<br>app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal'])<br>```<br><br>When specified, the IP addresses or the subnets are excluded from the address determination process, and the untrusted IP address nearest to the application server is determined as the client’s IP address.|
|Number|Trust the _n_th hop from the front-facing proxy server as the client.|
|Function|Custom trust implementation. Use this only if you know what you are doing.<br><br>```javascript<br>app.set('trust proxy', function (ip) {<br>  if (ip === '127.0.0.1' \| ip === '123.123.123.123') return true // trusted IPs<br>  else return false<br>})<br>```|


---
Created: March 8, 2024
Last Modified: `= this.file.mtime`

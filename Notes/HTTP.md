---
tags:
  - note
  - http
  - reference
  - HTTPstatus
---
# `= this.file.name `
---

#### Methods
---

[`GET`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)

The `GET` method requests a representation of the specified resource. Requests using `GET` should only retrieve data.

[`HEAD`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/HEAD)

The `HEAD` method asks for a response identical to a `GET` request, but without the response body.

[`POST`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)

The `POST` method submits an entity to the specified resource, often causing a change in state or side effects on the server.

[`PUT`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT)

The `PUT` method replaces all current representations of the target resource with the request payload.

[`DELETE`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE)

The `DELETE` method deletes the specified resource.

[`CONNECT`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/CONNECT)

The `CONNECT` method establishes a tunnel to the server identified by the target resource.

[`OPTIONS`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS)

The `OPTIONS` method describes the communication options for the target resource.

[`TRACE`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/TRACE)

The `TRACE` method performs a message loop-back test along the path to the target resource.

[`PATCH`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH)

The `PATCH` method applies partial modifications to a resource.

## Statuses
---
- ## 1×× Informational
    
- [100 Continue](https://httpstatuses.io/100)
- [101 Switching Protocols](https://httpstatuses.io/101)
- [102 Processing](https://httpstatuses.io/102)
- [103 Early Hints](https://httpstatuses.io/103)

- ## 2×× Success
    
- [200 OK](https://httpstatuses.io/200)
- [201 Created](https://httpstatuses.io/201)
- [202 Accepted](https://httpstatuses.io/202)
- [203 Non-authoritative Information](https://httpstatuses.io/203)
- [204 No Content](https://httpstatuses.io/204)
- [205 Reset Content](https://httpstatuses.io/205)
- [206 Partial Content](https://httpstatuses.io/206)
- [207 Multi-Status](https://httpstatuses.io/207)
- [208 Already Reported](https://httpstatuses.io/208)
- [226 IM Used](https://httpstatuses.io/226)

- ## 3×× Redirection
    
- [300 Multiple Choices](https://httpstatuses.io/300)
- [301 Moved Permanently](https://httpstatuses.io/301)
- [302 Found](https://httpstatuses.io/302)
- [303 See Other](https://httpstatuses.io/303)
- [304 Not Modified](https://httpstatuses.io/304)
- [305 Use Proxy](https://httpstatuses.io/305)
- [307 Temporary Redirect](https://httpstatuses.io/307)
- [308 Permanent Redirect](https://httpstatuses.io/308)

- ## 4×× Client Error
    
- [400 Bad Request](https://httpstatuses.io/400)
- [401 Unauthorized](https://httpstatuses.io/401)
- [402 Payment Required](https://httpstatuses.io/402)
- [403 Forbidden](https://httpstatuses.io/403)
- [404 Not Found](https://httpstatuses.io/404)
- [405 Method Not Allowed](https://httpstatuses.io/405)
- [406 Not Acceptable](https://httpstatuses.io/406)
- [407 Proxy Authentication Required](https://httpstatuses.io/407)
- [408 Request Timeout](https://httpstatuses.io/408)
- [409 Conflict](https://httpstatuses.io/409)
- [410 Gone](https://httpstatuses.io/410)
- [411 Length Required](https://httpstatuses.io/411)
- [412 Precondition Failed](https://httpstatuses.io/412)
- [413 Payload Too Large](https://httpstatuses.io/413)
- [414 Request-URI Too Long](https://httpstatuses.io/414)
- [415 Unsupported Media Type](https://httpstatuses.io/415)
- [416 Requested Range Not Satisfiable](https://httpstatuses.io/416)
- [417 Expectation Failed](https://httpstatuses.io/417)
- [418 I'm a teapot](https://httpstatuses.io/418)
- [421 Misdirected Request](https://httpstatuses.io/421)
- [422 Unprocessable Entity](https://httpstatuses.io/422)
- [423 Locked](https://httpstatuses.io/423)
- [424 Failed Dependency](https://httpstatuses.io/424)
- [425 Too Early](https://httpstatuses.io/425)
- [426 Upgrade Required](https://httpstatuses.io/426)
- [428 Precondition Required](https://httpstatuses.io/428)
- [429 Too Many Requests](https://httpstatuses.io/429)
- [431 Request Header Fields Too Large](https://httpstatuses.io/431)
- [444 Connection Closed Without Response](https://httpstatuses.io/444)
- [451 Unavailable For Legal Reasons](https://httpstatuses.io/451)
- [499 Client Closed Request](https://httpstatuses.io/499)

- ## 5×× Server Error
    
- [500 Internal Server Error](https://httpstatuses.io/500)
- [501 Not Implemented](https://httpstatuses.io/501)
- [502 Bad Gateway](https://httpstatuses.io/502)
- [503 Service Unavailable](https://httpstatuses.io/503)
- [504 Gateway Timeout](https://httpstatuses.io/504)
- [505 HTTP Version Not Supported](https://httpstatuses.io/505)
- [506 Variant Also Negotiates](https://httpstatuses.io/506)
- [507 Insufficient Storage](https://httpstatuses.io/507)
- [508 Loop Detected](https://httpstatuses.io/508)
- [510 Not Extended](https://httpstatuses.io/510)
- [511 Network Authentication Required](https://httpstatuses.io/511)
- [599 Network Connect Timeout Error](https://httpstatuses.io/599)


````ad-abstract
title: REST API


# HTTP Request Components in REST APIs

When interacting with a REST API, clients send HTTP requests to the server to perform various actions. An HTTP request typically consists of several components:

## 1. Request Line:
The request line is the first line of an HTTP request and contains three parts:
- **HTTP Method**: Specifies the action to be performed (e.g., GET, POST, PUT, DELETE).
- **Request URI (Uniform Resource Identifier)**: Identifies the resource on the server that the client wants to interact with.
- **HTTP Version**: Specifies the version of the HTTP protocol being used (e.g., HTTP/1.1).

## 2. Headers:
HTTP headers provide additional information about the request and the client making it. Some common headers used in REST API requests include:
- **Authorization**: Provides credentials for authenticating the client with the server.
- **Content-Type**: Specifies the media type of the request body (e.g., application/json, application/xml).
- **Accept**: Specifies the media types that the client is willing to accept in the response.
- **User-Agent**: Identifies the client software making the request (e.g., browser, mobile app).
- **Connection**: Specifies whether the connection should be kept alive for subsequent requests.

## 3. Request Body (Optional):
In some cases, HTTP requests may include a request body containing data to be sent to the server. This is common for operations like *creating* or *updating* resources. The format of the request body depends on the Content-Type header.

## Example HTTP Request:

```http
GET /users/123 HTTP/1.1
Host: example.com
Authorization: Bearer <access_token>
Accept: application/json
User-Agent: Mozilla/5.0
```
````

https://locall.host/how-to-use-postman-to-test-api-on-localhost/


---
Created: April 23, 2024
Last Modified: `= this.file.mtime`

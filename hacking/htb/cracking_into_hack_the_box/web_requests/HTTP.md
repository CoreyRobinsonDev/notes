# HyperText Transfer Protocol (HTTP)

## URL

![URL](https://academy.hackthebox.com/storage/modules/35/url_structure.png)
|Component|Example|Description|
|---|---|---|
|Scheme|http://https://|This is used to identify the protocol being accessed by the client, and ends with a colon and a double slash (`://`)|
|User Info|admin:password@|Contains the credentials separated by `:` used to authenticate to the host, and is separated from the host by (`@`)|
|Host|inlanefreight.com|The host signifies the resource location. This can be a hostname or IP address|
|Port|:80|`http` schemes default to port `80` and https defaults to port `443`|
|Path|/dashboard.php|Points to the resource being accessed. If no path is specified, the server returns `index.html`|
|Query String|?login=true|Consists of a parameter and a value. Multiple parameters can be separated by (`&`)|
|Fragments|#status|Processed by the borwser to locate sections within the resource|


![HTTP Flow](https://academy.hackthebox.com/storage/modules/35/HTTP_Flow.png)
## Headers

### General Headers
- **general headers** are used in both requests and repsonses
- they are contextual and are used to describe the message rather than its contents

|Header|Example|Description|
|---|---|---|
|Date|Date: Wed, 16 Feb 2022 10:38:44 GMT|Holds the date and time the message originated|
|Connection|Connection: close|Dictates if the current network connection should stay alive after the request|


### Entity Headers
- **entity headers** can be common on both request and response
- these headers are used to describe the content transferred by a message

|Header|Example|Description|
|---|---|---|
|Content-Type|Content-Type: text/html|Describes the type of resource being transferred|
|Media-Type|Media-Type: application/pdf|Describes the type of data being transferred|
|Boundary|boundary="b4e4fbd93540"|Acts as a marker to separate content when there is more than one in the same message|
|Content-Length|Content-Length: 385|Holds the size of the entity being passed|
|Content-Encoding|Content-Encoding: gzip|Type of encoding used in data transformations|

### Request Headers

|Header|Example|Description|
|---|---|---|
|Host|Host: www.inlanefreight.com|The host being queried for the resource|
|User-Agent|User-Agent: curl/7.77.0|Describes the client requesting resources|
|Referrer|Referrer: http://www.inlanefreight.com/|Denotes where the request is coming from|
|Accept|Accept: */*|Describes which media type the client can understand|
|Cookie|Cookie: PHPSESSID=b434fbd93540|A piece of data stored on the client and server that acts as an identifier|
|Authorization|Authorization: BASIC cGFzc3dvcmQK|A token stored on the client used as an identifier|

### Response Headers
|Header|Example|Description|
|---|---|---|
|Server|Server: Apache/2.2.14 (Win32)|Contains info about the HTTP server that processed the request|
|Set-Cookie|Set-Cookie: PHPSESSID=b434fbd93540|Contains teh cookies needed forlient indentification|
|WWW-Authenticate|WWW-Authenticate: BASIC realm="localhost"|Notifies the client about the type of authentication required to access the resource|

### Security Headers
- **security headers** are a class of response headers used to specify certain rules and policies to be followed by the browser

|Header|Example|Description|
|---|---|---|
|Content-Security-Policy|Content-Security-Policy: script-src 'self'|Dictates the policy towards externally injected resources, preventing XSS attacks|
|Strict-Transport-Security|Strict-Transport-Security: max-age=315360000|Forces all communication to be carried over HTTPS|
|Referrer-Policy|Referrer-Policy: origin|Dictates whether the client should include the value within the `Referrer` header|

# HTTPS

![HTTPS Flow](https://academy.hackthebox.com/storage/modules/35/HTTPS_Flow.png)


# HTTP Request

![HTTP Request](https://academy.hackthebox.com/storage/modules/35/raw_request.png)

|Field|Example|Description|
|---|---|---|
|Method|GET|The HTTP method or verb, which specifies the type of action to perform|
|Path|/users/login.html|The path to the resource|
|Version|HTTP/1.1|The HTTP version|

# HTTP Response

![HTTP Response](https://academy.hackthebox.com/storage/modules/35/raw_response.png)

# cURL (client URL)
- use `-O` to download the remote file
- use `-s` to silence the request status
- use `-k` to skip SSL certificate check
- use `-v` to print both the request and response
- use `-i` to print the header and body of the response
- use `-I` to send a **HEAD** request
- use `-H` to set request headers
- use `-A` to set the **User-Agent**
- use `-u` to provide credentials in **username:password** format


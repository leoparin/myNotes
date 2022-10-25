# 1 http:

## 1.1 what?
hypertext transfer protocal
超链接(hypertext is a word or words that contain a link to a website)传输协议

## 1.2 why?
与html结合实现web交互
用于在client跟server之间传送超链接

## 1.3 How?

^38e58a

格式：
 - 客户端：method、服务器地址、directory
 - 服务器：statue code
### 1.3.1 HTTP request:
几种请求method，根据不同的内容选择
不同请求内容适用不同的请求方法
要更新的内容有不同的要求，有时候更新局部，有时候更新整个
==POST:==请求一个你自己要求类型的数据（添加新城市天气）（200）提交表单
==GET==:请求
PUT:update 整个（注册）
patch：update局部（修改）
delete：

URI:
`http://<server_location>:<application_port>/<resource_path>`
URI=URL+path
URL:resource locator,identify the sever and the application

### 1.3.2 HTTP response:
server side
component:
1. response status:
- 2: correctly processed the request
- 4: something wrong with request
- 5: server went wrong
2. response header:used to transfer small amount of data(optional)
3. response body:
```html
HTTP/1.1 200 OK ❶

Server: Microsoft-IIS/4.0 ❷ 
Date: Mon, 14 May 2012 13:13:33 GMT ❷ 
Content-Type: text/html ❷ 
Last-Modified: Mon, 14 May 2012 13:03:42 GMT ❷ 
Content-Length: 112 ❷

<html> ❸ 
<head><title>HTTP Response</title></head>❸
<body>Hello Albert!</body> ❸ 
</html> ❸
```

### 1.3.3 http session
#### why?
system need to correlate some requests(shopping cart)
#### what?

#### how?
every requests should contain the same session id

# 2 html element
<th> :table head element

<span>: inline container,donot represent anything,for style usage

<br>:line break element



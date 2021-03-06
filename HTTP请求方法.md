## HTTP请求方法 ##

根据 HTTP 标准，HTTP请求可以使用多种请求方法。

HTTP1.0定义了三种请求方法：GET、POST和HEAD方法。

HTTP1.1新增了六种请求方法：OPTIONS、PUT、PATCH、DELETE、TRACE和CONNECT方法。

- GET：请求指定的页面信息主体。
- HEAD：类似GET请求，只不过返回的响应中没有具体的内容，用于获取报头。
- POST：向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立或已有资源的修改。
- PUT：从客户端向服务器传送的数据取代指定的文档内容。
- DELETE:请求服务器删除指定的页面。
- CONNECT：HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
- OPTIONS：允许客户端查看服务器的性能。
- TRACE：回显服务器收到的请求，主要用于测试或者诊断。
- PATCH：是对PUT方法的补充，用来对已知资源进行局部更新。


## HTTP响应头信息 ##

HTTP请求头提供了关于请求，响应或者其他的发送实体信息。

HTTP响应头信息详细介绍：

- Allow : 服务器支持哪些请求方法（如GET、POST等）。
- Content-Encoding : 文档编码（Encode）方法。只有在解码之后才可以得到Content-Type头指定的内容类型。利用gzip压缩文档能够显著的减少HTML文档的下载时间。Java的GZIPOutputStream 可以很方便的进行gzip压缩，但只有Unix上的Netscape和Window上的IE4,IE5才支持他，因此，Servlet应该通过查看Accept-Encoding头（即request.getHeader("Accept-Encoding")）检查浏览器是否支持gzip,为支持gzip的浏览器返回经gzip压缩的HTML页面，为其他浏览器返回普通页面。
- Content-Length : 表示内容的长度，只有当浏览器使用了持久HTTP连接时才需要这个数据。如果你想利用持久连接的优势，可以吧输出文档写入ByteArrayOutputStream，完成后查看其大小，然后把该值放入Content-Length头，最后通过byteArrayStream.writeTo(response.getOutputStream)发送内容。
- Contetnt-Type : 表示后面的文档属于什么MIME类型。Servlet默认为text/plain，但通常需要显式的指定为 text/html。由于经常要设置Content-Type,因此 HttpServletResponse 提供了一个专用的方法 setContentType。
- Date : 当前的GMT时间，你可以用 setDateHeader 来设置这个头以避免转换时间格式的麻烦、
- Expires : 应该在什么时候人为文档已经过期，从而不再缓存它？
- Last-Modified : 文档的最后改动时间。客户可以通过 if-Modified-Since请求头提供一个日期，该请求将被视为一个条件的GET，只有改动时间迟于指定时间的文档才会返回，否则返回一个304（NOT Modified）状态。Last-Modified也可用setDateHeader方法来设置。
- Location : 表示客户应当到哪里去取文档。Location通常不是直接设置的，而是通过HttpServletResponse的sendRedirect方法，该方法同时设置状态码为 302。
- 表示浏览器应该在多少时间之后刷新文档，以秒计。除了刷新当前文档之外，你还可以通过setHeader("Refresh","5; URL=http://host/path") 让浏览器读取指定的页面。  **注意** 在这种功能通常是通过设置HTML页面HEAD区的<META HTTP-EQUIV="Refresh" CONTENT="5;URL=http://host/path"> 实现，这是因为，自动刷新或重定向对于那些不能使用CGI或Servlet的HTML编写者十分重要。但是，对于Servlet来说，直接设置Refresh 头更加方便。   注意Refresh的意义是"N秒之后刷新本页面或者访问指定页面"，而不是"每隔N秒刷新本页面或访问指定页面"。因此，连续刷新要求每次都发送一个Refresh头，而发送204状态代码则可以组织浏览器联系刷新，不管是使用Refresh头还是<META HTTP-EQUIV="Refresh"...>。   **注意** Refresh头不属于 HTTP1.1正式规范的一部分，而是一个扩展，但Netscape和IE都支持他。
- Server : 服务器名字。Servlet 一般不设置这个值，而是由Web服务器自己设置。
- Set-Cookie : 设置和页面关联的Cookie。Servlet不应使用response.setHeader("Set-Cookie",...),而是应使用HttpServletResponse 提供的专用方法 addCookie。参见下文有关Cookie设置的讨论。
- WWW-Authenticate : 客户应该在 Authorization 头中提供什么类型的授权信息？在包含 401（Unauthorized） 状态行的应答中这个头是必须的，例如：response.setHeader("WWW-Authenticate","BASIC realm = \"executives\"")。**注意** Servlet 一般不进行着方面的处理，而是让Web服务器专门机制来控制受密码保护页面的访问（例如：.htaccess）


## HTTP状态码 ##

当浏览者访问一个网页时，浏览者的浏览器会向网页所在的服务器发送请求。当浏览器接收并显示网页前，此网页所在的服务器会返回一个包含HTTP状态码的信息头（server header）用以响应浏览器的请求。
HTTP状态码的英文为HTTP Status Code。
下面是常见的HTTP状态码：

- 200 - 请求成功
- 301 - 资源（网页等）被永久转移到其他URL
- 404 - 请求的资源（网页）不存在
- 500 - 内部服务器错误

## HTTP状态码分类 ##

HTTP状态码由三个十进制数字组成，第一个十进制数字定义了状态码的类型，后两个数字没有分类的作用，HTTP状态码分为5中类型。

- 1** ： 信息，服务器收到请求，需要请求者执行操作
- 2** ： 成功，操作被成功接收并处理
- 3** ： 重定向，需要进一步的操作以完成请求
- 4** ： 客户端错误，请求包含语法或无法完成请求
- 5** ： 服务器错误，服务器在处理请求的过程中发生错误

HTTP 状态码列表：

- 100 ： Continue 继续，客户端应继续其请求
- 101 ： Switching Protocols 切换协议，服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如：切换到 HTTP 的新版本协议。
- 200 ： OK 请求成功。一般用于GET和POST请求。
- 201 ： Created 已创建。成功请求并创建了新的资源。
- 202 ： Accepted 已接收。已经接收请求。但未处理完成。
- 203 ： Non-Authoritative Information  非授权信息，请求成功。但返回的 meta 信息不再原始的服务器，而是一个副本。
- 204 ： No Content 重置内容。服务器处理成功，单未返回内容。在未更新的网页的情况下，可确保浏览器继续显示当前文档
- 205 ： 充值内容。服务器处理成功，用户端（例如浏览器）应重置文档图。可通过此返回码清楚浏览器的表单域
- 206 ： Partial Content 部分内容。服务器成功处理了部分GET请求
- 300 ： 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择
- 301 ： Moved Permanently 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新的URI。今后任何新的请求都应用新的URI代替。
- 302 ： Found 临时移动。与301类似。使用GET和POST请求查看
- 303 ： See Other 查看其他地址，与301类似，使用GET和POST请求查看
- 304 ： Not Modified 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
- 305 ： Use Proxy 使用代理。所请求的资源必须通过代理访问
- 306 ： Unused 已经被废弃的HTTP状态码
- 307 ： Temporary Require 临时重定向，与302类似，使用GET请求重定向
- 400 ： Bad Request 客户端请求的语法错误，服务器无法理解
- 401 ： Unauthorized 请求要求用户的身份认证
- 402 ： Payment Reuqired 保留，将来使用
- 403 ： Forbidden 服务端理解请求客户的请求，单是拒绝执行请求
- 404 ： Not Found 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置 " 您所请求的资源无法找到 "的个性页面。
- 405 ： Method Not Allowed 客户端请求中的方法被禁止
- 406 ： Not Acceptable 服务器无法根据客户端请求的内容特性完成请求
- 407 ： Proxy Authentication Required 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权
- 408 ： Request Time-out 服务器等待客户端发送请求时间过长，超时
- 409 ： Conflict 服务器完成客户端的 PUT 请求时返回此代码，服务器处理请求时发生冲突
- 410 ： Gone 客户端请求的资源已经不存在。410不同于404，如果资源以前有 现在被永久删除了可使用410代码，网站设置人员可通过301代码指定资源的新位置
- 411 ： Length Required 服务器无法处理客户端发送的不带Content-Length的请求信息
- 412 ： Precondition Failed 客户端请求信息的先决条件错误
- 413 ： Request Entity Too Large 由于请求的实体过大，服务器无法处理，因此拒绝了请求。为防止客户端的连续请求，服务器可能会关闭连接。如果是服务器暂时无法处理，则会包含一个Retry-After的相应信息
- 414 ： Request-URL Too Large 请求的URL过长（URL通常为网址），服务器无法处理
- 415 ： Unsupported Media Type  服务器无法处理请求附带的媒体格式
- 416 ： Requested range not satisfiable 客户端请求的范围无效
- 417 ： Expectation Failed 服务器无法满足Expect请求头信息
- 500 ： Internal Server Error 服务器内部错误，无法完成请求
- 501 ： Not Implemented 服务器不支持请求功能，无法完成请求
- 502 ： Bad Gateway 作为代理公主的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应
- 503 ： Service Unavailable 由于超载或系统维护，服务器暂时无法处理客户端的请求，延时的长度可包含在服务器的Retry-After头信息中
- 504 ： Gateway Time-out 充当网关或代理服务器，未及时从远端服务器获取请求
- 505 ： HTTP Version not supported 服务器不支持请求的HTTP协议的版本，无法完成处理
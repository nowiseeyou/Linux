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
- 表示浏览器应该在多少时间之后刷新文档，以秒计。除了刷新当前文档之外，你还可以通过setHeader("Refresh","5; URL=http://host/path") 让浏览器读取指定的页面。  注意在这种功能通常是通过设置HTML页面HEAD区的<META HTTP-EQUIV="Refresh" CONTENT="5;URL=http://host/path"> 实现，这是因为，自动刷新或重定向对于那些不能使用CGI或Servlet的HTML编写者十分重要。但是，对于Servlet来说，直接设置Refresh 头更加方便。   注意Refresh的意义是"N秒之后刷新本页面或者访问指定页面"，而不是"每隔N秒"



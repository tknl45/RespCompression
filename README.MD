# Response compression application (ASP.NET Core 3.1)

* 啟用文字壓縮(文字檔/web api)
* 啟用圖片壓縮

## 參考
* https://docs.microsoft.com/zh-tw/aspnet/core/performance/response-compression?view=aspnetcore-5.0
* https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/performance/response-compression/samples


## Examples in this sample

* `BrotliCompressionProvider`
  * `text/plain`
    * **/testfile1kb.txt** - Text file response at 1,033 bytes that compresses to ~36 bytes.
* `GzipCompressionProvider`
  * `text/plain`
    * **/testfile1kb.txt** - Text file response at 1,033 bytes that compresses to ~47 bytes.
    * **/vue.js** - Text file response at 345.12 KB that compresses to ~107.1KB.
  * `image/svg+xml`
    * **/banner.svg** - A Scalable Vector Graphics (SVG) image response at 9,707 bytes that compresses to ~4,459 bytes.

When the request includes the `Accept-Encoding` header and response compression is successful, the middleware automatically adds a `Vary: Accept-Encoding` header to the response. The `Vary` header instructs caches to maintain multiple copies of the response based on alternative values of `Accept-Encoding`, so both a compressed (Gzip or Brotli) and uncompressed version are stored in caches for systems that can either accept the compressed or the uncompressed response.

## Use the sample

1. Make a request using [Fiddler](https://www.telerik.com/fiddler), [Firebug](https://getfirebug.com/), or [Postman](https://www.getpostman.com/) to the application without an `Accept-Encoding` header and note the response payload, response size, and response headers.
1. Add an `Accept-Encoding: br` or `Accept-Encoding: gzip` header and note the compressed response size and response headers. The response size drops, and the `Content-Encoding` response header is included by the middleware indicating that compression with either Gzip or Brotli occurred. When you look at the response body for the Lorem Ipsum or **testfile1kb.txt** response, you see that the text is compressed and unreadable.


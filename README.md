# urllib

urllib is an libs help you to curl remote url using golang.

## How to use?

### Example

```go
package main

import (
    "fmt"

    "github.com/GiterLab/urllib"
)

func main() {
    req := urllib.Get("http://tobyzxj.me/")
    req.Debug(true)
    str, err := req.String()
    if err != nil {
        fmt.Println(err)
    }
    fmt.Println(req.DumpRequestString()) // debug out
    fmt.Println(str)
}
```

### GET

you can use Get to crawl data.

```go
import "github.com/GiterLab/urllib"

str, err := urllib.Get("http://tobyzxj.me/").String()
if err != nil {
    // error
}
fmt.Println(str)
```

### POST

POST data to remote url

```go
req := urllib.Post("http://tobyzxj.me/")
req.Param("username","tobyzxj")
req.Param("password","123456")
str, err := req.String()
if err != nil {
    // error
}
fmt.Println(str)
```

### Set timeout

The default timeout is `60` seconds, function prototype:

```go
    SetTimeout(connectTimeout, readWriteTimeout time.Duration)
```

Exmaple:

```go
// GET
urllib.Get("http://tobyzxj.me/").SetTimeout(100 * time.Second, 30 * time.Second)

// POST
urllib.Post("http://tobyzxj.me/").SetTimeout(100 * time.Second, 30 * time.Second)
```

### Debug

If you want to debug the request info, set the debug on

```go
urllib.Get("http://tobyzxj.me/").Debug(true)
```

### Set HTTP Basic Auth

```go
str, err := Get("http://tobyzxj.me/").SetBasicAuth("user", "passwd").String()
if err != nil {
    // error
}
fmt.Println(str)
```

### Set HTTPS

If request url is https, You can set the client support TSL:

```go
urllib.SetTLSClientConfig(&tls.Config{InsecureSkipVerify: true})
```

More info about the `tls.Config` please visit <http://golang.org/pkg/crypto/tls/#Config>

### Set HTTP Version

some servers need to specify the protocol version of HTTP

```go
urllib.Get("http://tobyzxj.me/").SetProtocolVersion("HTTP/1.1")
```

### Set Cookie

some http request need setcookie. So set it like this:

```go
cookie := &http.Cookie{}
cookie.Name = "username"
cookie.Value  = "tobyzxj"
urllib.Get("http://tobyzxj.me/").SetCookie(cookie)
```

### Upload file

urllib support mutil file upload, use `req.PostFile()` or `req.PostFileFromReader()` to upload file.

```go
req := urllib.Post("http://tobyzxj.me/")
req.Param("username","tobyzxj")
req.PostFile("uploadfile1", "urllib.pdf")
str, err := req.String()
if err != nil {
    // error
}
fmt.Println(str)

// or
req := urllib.Post("http://tobyzxj.me/")
req.Param("username","tobyzxj")
req.PostFileFromReader("uploadfile1", "urllib.jpeg", "image/jpeg", fileReader)
str, err := req.String()
if err != nil {
    // error
}
fmt.Println(str)
```

See godoc for further documentation and examples.

* [godoc.org/github.com/GiterLab/urllib](https://godoc.org/github.com/GiterLab/urllib)

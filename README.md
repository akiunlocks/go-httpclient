## go-httpclient

**requires Go 1.1+** as of `v0.4.0` the API has been completely re-written for Go 1.1 (for a Go
1.0.x compatible release see [1adef50](https://github.com/mreiferson/go-httpclient/tree/1adef50))

[![Build
Status](https://secure.travis-ci.org/mreiferson/go-httpclient.png?branch=master)](http://travis-ci.org/mreiferson/go-httpclient)

Provides an HTTP Transport that implements the `RoundTripper` interface and
can be used as a built in replacement for the standard library's, providing:

 * connection timeouts
 * request timeouts

This is thin wrapper around http.Transport which set dial timeout and uses
time.AfterFunc to call the Go 1.1+ `CancelRequest()` API.

### Example

```go
transport := &httpclient.Transport{
    ConnectTimeout:        1*time.Second,
    RequestTimeout:        10*time.Second,
    ResponseHeaderTimeout: 5*time.Second,
}
defer transport.Close()

client := &http.Client{Transport: transport}
req, _ := http.NewRequest("GET", "http://127.0.0.1/test", nil)
resp, err := client.Do(req)
if err != nil {
    return err
}
defer resp.Body.Close()
```

### Reference Docs

For API docs see [godoc](http://godoc.org/github.com/mreiferson/go-httpclient).

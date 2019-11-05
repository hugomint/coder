+++
categories = ["http"]
date = 2019-10-30T14:00:00Z
slug = "http-server"
tags = ["server"]
title = "http server"

+++
#### Registering a Request Handler please

First, create a Handler which receives all in coming HTTP connections from browsers, HTTP clients or API requests. A handler in Go is a function with this signature:

    func (w http.ResponseWriter, r *http.Request)

The function receives two parameters:

* An http.ResponseWriter which is where you write your text/html response to.
* An http.Request which contains all information about this HTTP request including things like the URL or header fields.

#### Registering a request handler to the default HTTP Server is as simple as this:

    http.HandleFunc("/", func (w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hello, you've requested: %s\n", r.URL.Path)
    })

#### Listen for HTTP Connections

The request handler alone can not accept any HTTP connections from the outside. An HTTP server has to listen on a port to pass connections on to the request handler. Because port 80 is in most cases the default port for HTTP traffic, this server will also listen on it.

The following code will start Go’s default HTTP server and listen for connections on port 80. You can navigate your browser to http://localhost/ and see your server handing your request.

    http.ListenAndServe(":80", nil)
    
    package main
    
    import (
        "fmt"
        "net/http"
    )
    
    func main() {
        http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
            fmt.Fprintf(w, "Hello, you've requested: %s\n", r.URL.Path)
        })
    
        http.ListenAndServe(":80", nil)
    }
    
    package main
        import (
        "log"
        "net/http"
    )
    // Define a home handler function which writes a byte slice containing
    // "Hello from Snippetbox" as the response body.
    func home(w http.ResponseWriter, r *http.Request) {
        w.Write([]byte("Hello from Snippetbox"))
    }
    func main() {
    // Use the http.NewServeMux() function to initialize a new servemux, then
    // register the home function as the handler for the "/" URL pattern.
        mux := http.NewServeMux()
        mux.HandleFunc("/", home)
    // Use the http.ListenAndServe() function to start a new web server. We pass in
    // two parameters: the TCP network address to listen on (in this case ":4000")
    // and the servemux we just created. If http.ListenAndServe() returns an error
    // we use the log.Fatal() function to log the error message and exit. Note
    // that any error returned by http.ListenAndServe() is always non-nil.
        log.Println("Starting server on :4000")
        err := http.ListenAndServe(":4000", mux)
        log.Fatal(err)
    }
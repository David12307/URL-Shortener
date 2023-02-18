# URL Shortener

`main.go` is a Go program that provides a simple URL shortening service. It uses the `urlshort` package to redirect incoming HTTP requests to the appropriate destination URL.

## Usage

The program defines a `defaultMux` function that creates a new `http.ServeMux` and adds a single handler function to it. The `hello` function simply writes "Hello, world!" to the response writer.

```go
func defaultMux() *http.ServeMux {
    mux := http.NewServeMux()
    mux.HandleFunc("/", hello)
    return mux
}

func hello(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hello, world!")
}
```

The program then defines a map of paths to URLs, and creates a new http.HandlerFunc using the MapHandler function from the urlshort package. The MapHandler function is used to redirect requests for /urlshort-godoc and /yaml-godoc to their respective documentation sites, and to use the default handler function for all other requests.

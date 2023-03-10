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

The program then defines a map of paths to URLs, and creates a new `http.HandlerFunc` using the `MapHandler` function from the `urlshort` package. The `MapHandler` function is used to redirect requests for `/urlshort-godoc` and `/yaml-godoc` to their respective documentation sites, and to use the default handler function for all other requests.

```go
// Build the MapHandler using the mux as the fallback
pathsToUrls := map[string]string{
    "/urlshort-godoc": "https://godoc.org/github.com/gophercises/urlshort",
    "/yaml-godoc":     "https://godoc.org/gopkg.in/yaml.v2",
}
mapHandler := urlshort.MapHandler(pathsToUrls, mux)
```

The program then defines a YAML string that specifies a set of path/URL mappings, and creates a new `http.HandlerFunc` using the `YAMLHandler` function from the `urlshort` package. The `YAMLHandler` function is used to redirect requests for the paths specified in the YAML string to their respective URLs, and to use the `MapHandler` function as the fallback for all other requests.

```go
// Build the YAMLHandler using the mapHandler as the fallback
yaml := `
- path: /urlshort
  url: https://github.com/gophercises/urlshort
- path: /urlshort-final
  url: https://github.com/gophercises/urlshort/tree/solution
`
yamlHandler, err := urlshort.YAMLHandler([]byte(yaml), mapHandler)
if err != nil {
    panic(err)
}
```

Finally, the program starts a new HTTP server and listens for incoming requests.

```go
http.ListenAndServe(":8080", yamlHandler)
```

<img src="https://threedots.tech/go-in-one-evening/src/img-min/social.jpg" alt="gopher" width="100%" height="350">
# URL Shortener

`main.go` is a Go program that provides a simple URL shortening service. It uses the `urlshort` package to redirect incoming HTTP requests to the appropriate destination URL.

## Usage

The program defines a `defaultMux` function that creates a new `http.ServeMux` and adds a single handler function to it. The `hello` function simply writes "Hello, world!" to the response writer.

```
func defaultMux() *http.ServeMux {
    mux := http.NewServeMux()
    mux.HandleFunc("/", hello)
    return mux
}

func hello(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hello, world!")
}```

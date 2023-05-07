# Eleventy `pathPrefix` issue

As described in 11ty/eleventy-dev-server#56, redirects do not respect the `pathPrefix` option.

## Running

1. Clone this repository.
2. Run <kbd>npm ci</kbd>.
3. Run <kbd>npx @11ty/eleventy --serve</kbd>.
4. From another window, run <kbd>curl -i localhost:8080/prefix/test</kbd>.

Example output (`pathPrefix` is `/prefix`):

```
❯❯ curl -i localhost:8080/prefix/test/
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 169
Date: Sun, 07 May 2023 18:04:29 GMT
Connection: keep-alive
Keep-Alive: timeout=5

<script type="module" integrity="sha512-7Y25+FX/kRUbZEHtQBOSLffzofBxz8ABQErLAVpGkfzactkpJU5wtTmhIfIZeTw7VHg1JeTIC5kHkzPq7LqR1w==" src="/.11ty/reload-client.js"></script>

❯❯ curl -i localhost:8080/prefix/test
HTTP/1.1 301 Moved Permanently
Location: /test/
Date: Sun, 07 May 2023 18:04:30 GMT
Connection: keep-alive
Keep-Alive: timeout=5
Content-Length: 0
```

Note the incorrect `Location` header in the second response.

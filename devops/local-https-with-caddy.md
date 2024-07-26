# Local HTTPS with Caddy

Install [Caddy](https://caddyserver.com/docs/caddyfile).

Create a caddyfile:

```
myreactapp.caddy.localhost {
  reverse_proxy localhost:3000
}
```

Or:

```
{
  http_port 8800
  https_port 4444
}

rickandmorty.caddy.localhost:4444 {
  reverse_proxy localhost:4200
}

rickandmortyapi.caddy.localhost:4444 {
  reverse_proxy localhost:3004
}
```

- [Reverse Proxy](https://caddyserver.com/docs/caddyfile/directives/reverse_proxy#examples)
- [More about the Caddyfile](https://caddyserver.com/docs/caddyfile/concepts)

Use caddy via commandline: `caddy run`

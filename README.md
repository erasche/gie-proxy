# GIE Proxy

The Galaxy Interactive Environments proxy is a websocket aware HTTP proxy with
cookie based authentication.

## Features

- [x] Proxy HTTP + WS
- [x] Supports running under a proxy prefix
- [x] API to allow dynamically adding new proxy routes
- [x] save/restore proxy routes across restarts
- [ ] check for live routes (i.e. expect container death in background) regularly.
- [ ] kill routes after N minutes of no traffic
    - interesting case here, what if a container dies on the backend and
      another starts up between checks. That's unsettling, but could've
      happened with the NodeJS case as well.
- [ ] execute docker-compose kill/docker kills on route finish

## Building

First, make sure you have the Go build environment correctly installed. See
http://golang.org/ for more information.

Then run "make". This will in turn call the go utility to build the load
balancer, resulting in a binary named `gxproxy`


## Configuration

```
-api_key="THE_DEFAULT_IS_NOT_SECURE": Key to access the API
-cookie_name="galaxysession": cookie name
-listen="0.0.0.0:8080": address to listen on
-listen_path="/galaxy/gie_proxy": path to listen on (for cookies)
-storage="./session_map.json": Session map file. Used to (re)store route lists across restarts
```

## License

MIT Licensed. See the file LICENSE for license information.

Based on code from https://github.com/akrennmair/drunken-hipster, however a
substantial rewrite took place, leaving only a small portion of the original
code base intact (the copy/plumbing functions in util.go).

# Response Creators

A collection of factory functions for [Fetch API](https://developer.mozilla.org/docs/Web/API/Response) `Response` types with pre-filled status and status-text headers for [well-known HTTP status codes](https://developer.mozilla.org/docs/Web/HTTP/Status).

It is meant to be used in Service Workers and/or Cloudflare Workers.

```js
import { ok } from '@werker/response-creators'

self.addEventListener('fetch', event => event.respondWith(ok()))
```

For the most part, factory functions can be used like regular `Response` constructors, e.g. 

```js
event.respondWith(
  ok('Your custom body init', { headers: { 'Content-Type': 'text/plain' } })
)
```

However, some provide a slightly different interface for enhanced usability. E.g. redirects (300, 301, 302, 303, 307, 308):

```js
event.respondWith(
  seeOther(`/your-redirect-url`)
)
```

(This will set the `Location` header to `/your-redirect-url`).

**NOTE**: When using JSON response bodies, consider combining it with [`worker-tools/json-fetch`](https://github.com/worker-tools/json-fetch) like so:

```js
event.respondWith(
  new JSONResponse({ error: '...' }, badRequest())
)
```

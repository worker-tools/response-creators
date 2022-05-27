# Response Creators

A collection of factory functions for [Fetch API](https://developer.mozilla.org/docs/Web/API/Response) `Response` types with pre-filled status and status-text headers for [well-known HTTP status codes](https://developer.mozilla.org/docs/Web/HTTP/Status).

It is meant to be used in Service Workers and/or Cloudflare Workers.

```js
import { ok } from '@worker-tools/response-creators'

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

Due to signature of the `Response` constructor, the opposite order (`badRequest(new JSONResponse({ error: '...' }))`) does not work!

--------

<p align="center"><a href="https://workers.tools"><img src="https://workers.tools/assets/img/logo.svg" width="100" height="100" /></a>
<p align="center">This module is part of the Worker Tools collection<br/>⁕

[Worker Tools](https://workers.tools) are a collection of TypeScript libraries for writing web servers in [Worker Runtimes](https://workers.js.org) such as Cloudflare Workers, Deno Deploy and Service Workers in the browser. 

If you liked this module, you might also like:

- 🧭 [__Worker Router__][router] --- Complete routing solution that works across CF Workers, Deno and Service Workers
- 🔋 [__Worker Middleware__][middleware] --- A suite of standalone HTTP server-side middleware with TypeScript support
- 📄 [__Worker HTML__][html] --- HTML templating and streaming response library
- 📦 [__Storage Area__][kv-storage] --- Key-value store abstraction across [Cloudflare KV][cloudflare-kv-storage], [Deno][deno-kv-storage] and browsers.
- 🆗 [__Response Creators__][response-creators] --- Factory functions for responses with pre-filled status and status text
- 🎏 [__Stream Response__][stream-response] --- Use async generators to build streaming responses for SSE, etc...
- 🥏 [__JSON Fetch__][json-fetch] --- Drop-in replacements for Fetch API classes with first class support for JSON.
- 🦑 [__JSON Stream__][json-stream] --- Streaming JSON parser/stingifier with first class support for web streams.

Worker Tools also includes a number of polyfills that help bridge the gap between Worker Runtimes:
- ✏️ [__HTML Rewriter__][html-rewriter] --- Cloudflare's HTML Rewriter for use in Deno, browsers, etc...
- 📍 [__Location Polyfill__][location-polyfill] --- A `Location` polyfill for Cloudflare Workers.
- 🦕 [__Deno Fetch Event Adapter__][deno-fetch-event-adapter] --- Dispatches global `fetch` events using Deno’s native HTTP server.

[router]: https://workers.tools/router
[middleware]: https://workers.tools/middleware
[html]: https://workers.tools/html
[kv-storage]: https://workers.tools/kv-storage
[cloudflare-kv-storage]: https://workers.tools/cloudflare-kv-storage
[deno-kv-storage]: https://workers.tools/deno-kv-storage
[kv-storage-polyfill]: https://workers.tools/kv-storage-polyfill
[response-creators]: https://workers.tools/response-creators
[stream-response]: https://workers.tools/stream-response
[json-fetch]: https://workers.tools/json-fetch
[json-stream]: https://workers.tools/json-stream
[request-cookie-store]: https://workers.tools/request-cookie-store
[extendable-promise]: https://workers.tools/extendable-promise
[html-rewriter]: https://workers.tools/html-rewriter
[location-polyfill]: https://workers.tools/location-polyfill
[deno-fetch-event-adapter]: https://workers.tools/deno-fetch-event-adapter

Fore more visit [workers.tools](https://workers.tools).

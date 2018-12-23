- net.Socket is a duplex stream
- socket events: 'lookup' then 'connect'
- socket events: 'end' then 'close'

- http.Server -> 'request' (req, res) -> 'finish' -> `res.end` callback
- http.ClientRequest (writable stream) -> 'response' http.IncomingMessage -> 'data'
  - `res` is http.IncomingMessage because this "makes" a request (it is a client) hence the server (remote) response is the incoming message
  - if 'response' handler is added the data from the response object must be consumed otherwise the 'end' event will not be fired - lead to memory leak

- http.IncomingMessage (**readable stream**)
  - http.Server 'request' (req)
  - http.ClientRequest 'response' (res)
- http.ServerResponse (**writable stream**)
  - http.Server 'request' (res)

http://book.mixu.net/node/ch10.html

- headers must be sent before the request data
- headers is sent when `res.writeHead` is called
- `res.writeHead` must be called *only once* and before `res.end`
- `Content-Length` is given in bytes not characters - use `Buffer.byteLength(content)` to get the length
- without `res.writeHead` calling `res.write` will set and send implicit header



## Architect Node App (Finished)

https://medium.com/@zurfyx/building-a-scalable-node-js-express-app-1be1a7134cfd
good reference to get good ideas, not perfect though


## Architect Node App (To Read)

- n/a


## Koa (Finished)

https://strongloop.com/strongblog/node-js-express-introduction-koa-js-zone/
- good reference for beginner (different ways to work with "co" and generator)


## HTTP & Streams API (Finished)

https://nodejs.org/en/docs/guides/anatomy-of-an-http-transaction/#sending-response-body
- `req` is an instance of `class IncomingMessage extends ReadableStream /* interface */`
- It's important to note here that all headers are represented in lower-case only, regardless of how the client actually sent them. This simplifies the task of parsing headers for whatever purpose. Cache-Control is available in `headers['cache-control']`, myRandomHeader is available in `headers.myrandomheader`.
- It's important to set the status and headers (`res.writeHead`) before you start writing chunks of data to the body (`res.write`).

https://medium.freecodecamp.org/understanding-node-js-event-driven-architecture-223292fcbc2d
https://nodejs.org/en/docs/guides/backpressuring-in-streams/
- advanced concept on backpressuring - review when I work with node streams more


## Event Loop (Finished) 

https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/


## Open Questions

- how does the `http` module handles `req.headers` when no header is sent
- what are some best practices to handle errors in nodejs streams?


## Node Stream

- ReadableStream: to read data _from_ (readable ->)
- WritableStream: to write data _to_ (-> writable)
- [Stream Fundamental](https://medium.freecodecamp.org/node-js-streams-everything-you-need-to-know-c9141306be93)
- [Streaming Chunked HTML - StrongLoop 2014](https://strongloop.com/strongblog/streaming-chunked-html-node-js-data/)

# Go Example for TurboStreams over WebSockets

Simple example for using [Turbo](https://turbo.hotwire.dev/)s [Stream](https://turbo.hotwire.dev/reference/streams)s in Go with the [Gorilla WebSocket](https://github.com/gorilla/websocket) toolkit.

Run the sample using the following command:

    $ go run *.go

To use the chat example, open http://localhost:8080/ in your browser.

## Frontend
The frontend connects to the Turbo Stream using plain JavaScript like:

```html
<script src="https://unpkg.com/@hotwired/turbo@7.0.0-beta.1/dist/turbo.es5-umd.js" ></script>
<script>
Turbo.connectStreamSource(new WebSocket("ws://" + document.location.host + "/ws"));
</script>
```

After that the frontend is connected to the Turbo Stream and get's all messages. Every chat message is appended to the dom element with id `board`.

This _should_ work with html markup too but I have not gotten it working yet.

## Server

The server receives the new chat message via web socket. Then it wraps the message as Turbo Stream action with action `append` and broadcasts it to all subscribers. That way all subscribed users see the new message on the board.

The raw text message sent over the web socket is:
```json
{ 
  "identifier": 
     "{\"channel\":\"Turbo::StreamsChannel\",  gned_stream_name\":\"**mysignature**\"}",
  "message":
    "<turbo-stream action="append" target="board">
  	<template>
  		<p>My ne wMessage</p>
  	</template>
     </turbo-stream>"
}
```

## Credits

Based on [Gorilla WebSocket Chat Example](https://github.com/gorilla/websocket/tree/master/examples/chat)

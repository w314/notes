# Socket Programming with `net` module
> With the `net module` we can create `TCP servers` and do `socket programming`.

Use cases:
- chat applications
- live streaming of audio/video

## TCP Server

- listens for connections from its clients
- also sends data to the clients

`tcpServer.js`
```js
// import the net module
import net from "node:net";

// create TCP server

// takes function as argument with client object as parameter
const tcpServer = net.createServer((client) => {
  console.log("Client connected.");

  // listening to data event to get data from the client
  client.on('data', (data) => {
    // use write method to send message to the client
    client.write(`Received following data: ${data}`);
  });

  // listening to close event which means the client is disconnected
  client.on('close', () => console.log(`Client disconnected.`));
});

// start TCP server
const port = 1234;
tcpServer.listen(port, () =>
  console.log(`TCP server listening on port ${port}`)
);
```

## TCP Clients

- connects to the TCP server
- exchanges data with the TCP server

`tcpClient.js`
```js
// import the net module
import net from "node:net";

// create client that connects to tcp server
const client = net.connect({ port: 1234 }, () => {
  console.log(`Connected to tcp server`);
  // sending messages to the server
  client.write(`Message from client`);
});

// listen to data event to get data from tcp server
client.on("data", (data) => {
  console.log(`Message received from server: ${data}`);
});

// commented out as gives write after end error
// disconnect from tcp server
// client.end();
// listen to end event to log `Disonnected from server`
// client.on('end', () => console.log(`Disconnected from server`));
```
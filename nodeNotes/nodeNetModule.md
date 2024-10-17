# Socket Programming with `net` module

Net module is and asynchronous wrapper for socket programming.


## TCP Server

tcpServer.js
```js
import net from 'node:net';

// create TCP server
// takes function as argument with client object as parameter
const tcpServer = net.createServer( (client) => {
    console.log('Client connected.');

    // listening to data event to get data from the client
    client.on('data', (data) => {
        // sends message to client
        client.write(data);
    })

    // listening to close event which means the client is disconnected
    client.on('close', () => console.log(`Client disconnected.`));
});

// start TCP server
const port = 1234;
tcpServer.listen(port, () => console.log(`TCP server listening on port ${port}`));
```

## TCP Client

tcpClient.js
```js
import net from 'node:net';

// create client that connects to tcp server
const client = net.connect({ port: 1234 }, () => {
    console.log(`Connected to tcp server`);
    // sending message to the server
    client.write(`<B>Name:</B> ${chatname}`);
    client.write(`<br><B>Message:</B> ${chatmessage}`);
})

// listen to data event to get data from tcp server
client.on('data', (data) => {
    console.log(`Message received from server: ${data.toString()}`);
})

// disconnect from tcp server
client.end();
client.on('end', () => console.log('Disconnected from server'));
```
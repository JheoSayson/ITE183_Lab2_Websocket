# ITE183 Lab 2: WebSocket Server

A real-time multi-client chat server written in **Bonezegei Scripting Language (BSL) v1.3.3**.
The same server on port `8000` serves static HTML pages over HTTP and upgrades connections to
WebSocket for full-duplex chat.

## Features

- Serves `public/index.html` at `/` and a custom `public/404.html` for any other route
- WebSocket connection lifecycle handling: connect, receive data, disconnect, each with its own client ID
- Sends a welcome message to a newly connected client
- Broadcasts every received message to all connected clients with `server.sendAll()`
- Browser chat client that shows connection status and a sent/received message log

## Project Structure

```text
ITE183_Lab2_Websocket/
├── app.bzg            # HTTP + WebSocket server
├── package.json       # project metadata and the `http` dependency
├── lib/               # BSL http library (installed by `bzg install`)
│   ├── http.bzg
│   ├── http.json
│   └── http/http.dll
├── public/
│   ├── index.html     # WebSocket chat client
│   └── 404.html       # custom 404 page
├── documentation/     # screenshots for the lab report
├── .gitattributes     # *.bzg linguist-language=JavaScript
├── LICENSE            # MIT
└── README.md
```

## Requirements

- Bonezegei Scripting Language v1.3.3 (verify with `bonezegei -v`)
- A modern web browser

## Installation and Usage

```bash
bzg install     # install dependencies
bzg run         # start the server (runs `bonezegei app.bzg`)
```

Then open <http://localhost:8000> in two or more browser windows and chat between them.
Open any other path (for example <http://localhost:8000/missing>) to see the custom 404 page.
Stop the server with `Ctrl+C`.

## How It Works

| Event | Handler | Behavior |
| --- | --- | --- |
| HTTP GET | `server.get(path, data)` | Serves `public/index.html` for `/`, otherwise `public/404.html` |
| WebSocket connect | `server.onConnect(clientId)` | Logs the client ID and sends a welcome message |
| WebSocket message | `server.onData(message, clientId)` | Logs the message and broadcasts it to everyone with `server.sendAll()` |
| WebSocket disconnect | `server.onDisconnect(clientId)` | Logs the disconnected client ID |

## Screenshots

Screenshots are in the `documentation/` folder:

1. `bonezegei -v` showing version 1.3.3
2. `bzg install` and `bzg run` (server startup)
3. Two browser windows exchanging messages in real time
4. The custom 404 page

## Author

Jheo Sayson, MSU-IIT, ITE183 Web Systems and Technologies

## License

Released under the [MIT License](LICENSE).
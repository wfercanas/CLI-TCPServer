# CLI - TCP Server

## Project Description

This project creates two simple servers (one of them concurrent using Goroutines) and a client using the Command Line as their interfaces.

- The server that is not concurrent receives commands from the client and returns the current date.
- The server that is concurrent receives commands from the client and returns the total amount of clients that it has served.

## How to use

1. First of all you need to have Go installed in your machine. For info about this point go to the [Download](https://go.dev/dl/) page of the official site.
2. Clone this repo in your computer: `git clone`
3. **Server**: Open a session in your terminal, go to the project folder and run the server: `go run ./server/server.go 3000`. This will make your server listen through the port 3000. This server handles only one client at a time.
4. **Client**: Open a new session in your terminal, go to the project folder and run the client: `go run ./client/client.go 127.0.0.1:3000`. This will create a connection with the server you are running in local and listening the port 3000.
5. **Close connection**: To close the connection, use the command "STOP" in the Client. This will close the server and the client.
6. **Concurrent Server** Open a session in your terminal, go to the project folder and run the server: `go run ./concurrentServer/concurrentServer.go 3000`. This will make your server listen also through the port 3000 (make sure the other server is not working or use another port, like 3001).
7. **Clients**: To connect multiple clients to the concurrent server you need to open multiple terminal sessions and run as many clients as you want using the same instructions already given. Using the command "STOP" you can still close the connection of the client, but this won't shut down the server. To do so, you will need to use CTRL+C in the server session.

## Key Concepts

To make this project work, you need to import some libraries and use certain functions. I will explain some of them:

**General**

- `os.Args` reads the extra arguments you use when you run the servers or clients. In this case we use this to define the host and port we'll be listening to.

**Client**

- `net.Dial()` begins the implementation of TCP Clients and helps you get connected to a desired server.
- `bufio.NewReader(os.Stdin)` creates a reader linked to the terminal, so we can read and then use what the user types in.
- `Fprintf()` is a method from `fmt` that we will use to send the user input to the TCP Server.
- `bufio.NewReader(connection)` helps us now to read the server response.

**Server**

- `net.Listen()` makes a program act as a TCP Server. The function returns a Listener variable.
- `listener.Accept()` enables the listener to start a connection with a client.
- `connection.Write()` allows us to write responses in the connection for the client to receive them.
- `go handleConnection()` allows us to serve multiple clients through the use of goroutines. The keyword `go` allows us to execute the function concurrently for all the clients.

## Acknowledgements

Thanks to Linode for the amazing article about Go, one of which is the implementation of this project. You can check the article [here](https://www.linode.com/docs/guides/developing-udp-and-tcp-clients-and-servers-in-go/).

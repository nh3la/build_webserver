HTTP webserver in C. 
project overview
This project is a simple HTTP server built in C to explore low-level network programming and client-server communication. It uses sockets to listen for TCP connections, receive HTTP requests, and send a simple text response. When a client visits the server on port 2900, the program responds with HTTP status 200 OK and the message hello!. The project emphasizes understanding how a basic web server works rather than relying on a web framework.
how the code works
The application consists of three source files that separate networking operations from the response logic:
- http-server.h defines the start_server() function interface and a BUFFER_SIZE constant of 2048 bytes. It also includes the system headers needed for socket programming.
- http-server.c implements start_server(), which creates a socket with socket(), enables SO_REUSEADDR, and binds the socket to the requested port on available network interfaces. It then calls listen() to prepare for incoming connections. A loop uses accept() to establish a client connection, recv() to read the request into a buffer, and a callback function to generate the response. After handling each request, it closes that client's socket.
- string-server.c supplies the callback and application entry point. Its main() function starts the server on port 2900 by passing handle() to start_server(). The handle() function prints the incoming request to the terminal and uses write() to send an HTTP response header followed by hello!.
The function-pointer callback allows the networking code to remain separate from the specific content returned to clients. This structure also makes it easier to experiment with other response handlers without rewriting the socket setup.


Build and Run
gcc http-server.c string-server.c -o server
./server
In another terminal run
curl http://localhost:2900
then it should say hello!

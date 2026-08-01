# 3b.CREATION FOR CHAT USING TCP SOCKETS
## AIM
To write a python program for creating Chat using TCP Sockets Links.
## ALGORITHM:
1. Import the necessary modules in python
2. Create a socket connection to using the socket module.
3. Send message to the client and receive the message from the client using the Socket module in
 server
4. Send and receive the message using the send function in socket.
## PROGRAM
## SERVER SIDE:
```
import socket


def start_server():
    # Define host and port
    host = "127.0.0.1"  # Localhost
    port = 5000  # Non-privileged port

    # Create a TCP/IP socket
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Bind the socket to the port
    server_socket.bind((host, port))

    # Listen for incoming connections (max 1 queued connection)
    server_socket.listen(1)
    print(f"Server started on {host}:{port}. Waiting for a client to connect...")

    # Accept connection from client
    client_socket, client_address = server_socket.accept()
    print(f"Connection established with: {client_address}\n")

    while True:
        # Receive data from the client (buffer size = 1024 bytes)
        client_message = client_socket.recv(1024).decode()

        if not client_message or client_message.lower() == "bye":
            print("Client disconnected.")
            break

        print(f"Client: {client_message}")

        # Send a response to the client
        server_message = input("Server: ")
        client_socket.send(server_message.encode())

        if server_message.lower() == "bye":
            print("Chat ended by server.")
            break

    # Close the sockets
    client_socket.close()
    server_socket.close()


if __name__ == "__main__":
    start_server()
```
## CLIENT SIDE:
```
import socket


def start_client():
    host = "127.0.0.1"  # Server's IP address (Localhost)
    port = 5000  # Server's port number

    # Create a TCP/IP socket
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Connect to the server
    client_socket.connect((host, port))
    print("Connected to the server! Type 'bye' to exit.\n")

    while True:
        # Input message to send to server
        client_message = input("Client: ")
        client_socket.send(client_message.encode())

        if client_message.lower() == "bye":
            print("Chat ended by client.")
            break

        # Receive response from server
        server_message = client_socket.recv(1024).decode()

        if not server_message or server_message.lower() == "bye":
            print("Server disconnected.")
            break

        print(f"Server: {server_message}")

    # Close the connection
    client_socket.close()


if __name__ == "__main__":
    start_client()
```
## OUPUT
## SERVER SIDE:
<img width="959" height="500" alt="image" src="https://github.com/user-attachments/assets/1510662f-f1a6-4d24-91b2-f024c7f00365" />

## CLIENT SIDE:
<img width="959" height="522" alt="image" src="https://github.com/user-attachments/assets/f9c5f6c4-c834-414b-b8e5-80d40f4a39f2" />

## RESULT
Thus, the python program for creating Chat using TCP Sockets Links was successfully 
created and executed.

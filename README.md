# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
client.py
```
import socket

s = socket.socket()
host = socket.gethostname()
port = 60000

s.connect((host, port))
s.send("Hello server!".encode())

with open('received_file.txt', 'wb') as f:
    while True:
        print("receiving data...")
        data = s.recv(1024)
        print("data=%s" % data)

        if not data:
            break

        f.write(data)

print("Successfully get the file")
s.close()
print("connection closed")
```

server.py
```
import socket
import os

port = 60000
s = socket.socket()
host = socket.gethostname()

s.bind((host, port))
s.listen(5)

print(f"Server listening on {host}:{port}")

while True:
    conn, addr = s.accept()
    print("Got connection from", addr)

    data = conn.recv(1024)
    print("Server received:", repr(data))

    filename = 'mytext.txt'

    if not os.path.exists(filename):
        print(f"ERROR: {filename} does not exist. Please place it in the same folder.")
        conn.send("File not found on server".encode())
        conn.close()
        continue

    with open(filename, 'rb') as f:
        l = f.read(1024)
        while l:
            print("Sent ", repr(l))
            conn.send(l)
            l = f.read(1024)

    print("Done sending")
    conn.send("Thank you for connecting".encode())
    conn.close()
```
## OUTPUT
```
server-side output
```
<img width="640" height="202" alt="image" src="https://github.com/user-attachments/assets/f862d41e-4226-4923-8bb9-e8902865c1ea" />

```
client-side output
```
<img width="794" height="264" alt="image" src="https://github.com/user-attachments/assets/6d7967db-0ab6-4b4e-b6ce-6c30a853a199" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.

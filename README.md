# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

client side:
```
import socket

c = socket.socket()
c.connect(('localhost', 9999))

n = int(input("No. of frames: "))
w = int(input("Window size: "))
frames = list(range(n))

i = 0
while i < n:
    send = frames[i:i+w]
    print("Sending:", send)
    c.send(str(send).encode())

    ack = c.recv(1024).decode()
    print("ACK:", ack)
    i += w

c.close()
```

Server side

```
import socket

s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server ready...")

c, _ = s.accept()
while True:
    data = c.recv(1024).decode()
    if not data:
        break

    print("Received:", data)
    c.send(f"ACK: {data}".encode())

c.close()
s.close()
```
## OUTPUT

<img width="950" height="306" alt="image" src="https://github.com/user-attachments/assets/6e1e3ef7-b846-492c-ba5f-2f835c82986e" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

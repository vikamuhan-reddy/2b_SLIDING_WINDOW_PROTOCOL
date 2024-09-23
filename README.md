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
### Server-sliding
```py
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
   frames = conn.recv(1024).decode()
   if not frames:
       break

   print(f"Received frames: {frames}")
   ack_message = f"ACK for frames: {frames}"
   conn.send(ack_message.encode())

conn.close()  
s.close()  
```
### Client-sliding
```py
import socket
c = socket.socket()
c.connect(('localhost', 9999))
size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))
i = 0
while True:
   while i < len(l):
       st = i + s
       frames_to_send = l[i:st]  
       print(f"Sending frames: {frames_to_send}")
       c.send(str(frames_to_send).encode())  

       ack = c.recv(1024).decode()  
       if ack:
           print(f"Acknowledgment received: {ack}")
           i += s  
   break
c.close()  
```

## OUPUT
### Server
<img width="703" alt="Screen Shot 1946-07-01 at 20 49 40" src="https://github.com/user-attachments/assets/1bf63bcc-03e9-417c-942e-7b19f3488ce9">

### Client
<img width="900" alt="Screen Shot 1946-07-01 at 20 52 03" src="https://github.com/user-attachments/assets/c9df06ec-b49e-4a4d-a4fd-9b56b7e994d7">

## RESULT

Thus, python program to perform stop and wait protocol was successfully executed

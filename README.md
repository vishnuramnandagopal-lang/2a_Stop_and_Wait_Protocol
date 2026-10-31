# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
Server
~~~
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server ready...")

c, _ = s.accept()

while True:
    msg = c.recv(1024).decode()
    if not msg:
        break

    print("Received:", msg)
    c.send(b"ACK")

    if msg == "exit":
        break

c.close()
s.close()
~~~
client
~~~
import socket

c = socket.socket()
c.connect(('localhost', 8000))
c.settimeout(5)

while True:
    msg = input("Message: ")
    c.send(msg.encode())

    if msg == "exit":
        break

    try:
        if c.recv(1024).decode() == "ACK":
            print("ACK received")
    except socket.timeout:
        print("No ACK, retransmitting...")

c.close()
~~~
## OUTPUT
server
<img width="442" height="201" alt="image" src="https://github.com/user-attachments/assets/b4576484-0337-409d-a856-20d03863e801" />

client
<img width="467" height="236" alt="image" src="https://github.com/user-attachments/assets/e0cdb99c-796d-4f5b-ba15-08ab98aefbbf" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.

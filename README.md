# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
cli.py
```
import socket
c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":  
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()

```
ser.py
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:  
        break

    try:
        mac = address[ip]  # Get the MAC address for the IP
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())  
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())
c.close()
s.close()
```

## OUPUT - ARP

<img width="1919" height="1138" alt="Screenshot 2025-09-19 113341" src="https://github.com/user-attachments/assets/aa99c5a3-e166-4c5a-a3cb-ee2a9d09d4b3" />

## PROGRAM - RARP
se.py
```
import socket 
s=socket.socket() 
s.connect(('localhost',9000)) 
while True:
 ip=input("Enter MAC Address : ")
 s.send(ip.encode())
 print("Logical Address",s.recv(1024).decode())
```
cl.py
```
import socket
s=socket.socket()
s.bind(('localhost',9000)) 
s.listen(5)
c,addr=s.accept()
address={"6A:08:AA:C2":"192.168.1.100","8A:BC:E3:FA":"192.168.1.99"};
while True:
 ip=c.recv(1024).decode() 
 try:
  c.send(address[ip].encode())
 except KeyError:
  c.send("Not Found".encode())
```
## OUPUT -RARP
<img width="1919" height="1142" alt="Screenshot 2025-09-19 114333" src="https://github.com/user-attachments/assets/86954124-6596-4c5b-af12-23e500c75461" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.

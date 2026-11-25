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

## CREATED BY : KARTHIKA AJAN
## REGISTER NUMBER : 212225100021

## PROGRAM - ARP
server
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")
c, addr = s.accept()
print(f"Connection established with {addr}")
address = {
    "192.168.1.5": "3c:22:fb:1a:9c:4e",
    "192.168.1.10": "08:92:4c:ef:21:7b",
}
while True:
    ip = c.recv(1024).decode()
    if not ip or ip.lower() == "exit":
        print("Client disconnected.")
        break
    try:
        mac = address[ip]  # Get the MAC address for the IP
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("MAC Address Not Found".encode())
c.close()
```
client
```
import socket
c = socket.socket()
c.connect(('localhost', 8000))
while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")
    c.send(ip.encode())
    if ip.lower() == "exit":
        break
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()
```
## OUPUT - ARP
<img width="1625" height="281" alt="Screenshot 2025-09-29 131248" src="https://github.com/user-attachments/assets/c18b20b9-7717-4385-b771-130b8a423645" />


## PROGRAM - RARP
server
```import socket
s = socket.socket()
s.bind(('localhost', 5000))
s.listen(5)
print("Server is listening...")
c, addr = s.accept()
print(f"Connection established with {addr}")
address = {"3c:22:fb:1a:9c:4e": "192.168.1.5","08:92:4c:ef:21:7b": "192.168.1.10"}
while True:
    mac = c.recv(1024).decode()
    if not mac or mac.lower() == "exit":
        print("Client disconnected.")
        break
    try:
        ip = address[mac]
        print(f"MAC: {mac} -> IP: {ip}")
        c.send(ip.encode())
    except KeyError:
        print(f"MAC: {mac} not found in ARP table.")
        c.send("Not Found".encode())
c.close()
```
client
```
import socket
s = socket.socket()
s.connect(('localhost', 5000))
while True:
    mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
    s.send(mac.encode())
    if mac.lower() == "exit":
        break
    ip = s.recv(1024).decode()
    print(f"IP Address for {mac}: {ip}")
s.close()
```
## OUPUT -RARP

<img width="1529" height="278" alt="image" src="https://github.com/user-attachments/assets/85409c3b-f011-42f5-8b7f-1e0a5d1e21ad" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.

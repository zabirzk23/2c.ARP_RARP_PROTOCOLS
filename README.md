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

## PROGRAM - RARP
server rarp
```
# rarp_server.py
import socket

# Predefined RARP table (MAC -> IP)
rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(("localhost", 9998))
server_socket.listen(1)

print("RARP Server is running...")

conn, addr = server_socket.accept()
print(f"Connection from {addr}")

while True:
    mac_address = conn.recv(1024).decode()
    if not mac_address:
        break
    print(f"Received MAC: {mac_address}")

    ip_address = rarp_table.get(mac_address, "IP not found")
    conn.send(ip_address.encode())

conn.close()
server_socket.close()
```
client rarp
```
# rarp_client.py
import socket

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(("localhost", 9998))

mac_address = input("Enter MAC Address to find IP: ")
client_socket.send(mac_address.encode())

ip_address = client_socket.recv(1024).decode()
print(f"IP Address for {mac_address} is: {ip_address}")

client_socket.close()
```
## OUPUT -RARP

<img width="1856" height="1097" alt="image" src="https://github.com/user-attachments/assets/1f36515a-ca93-4482-8f10-1a74c4bec15d" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.

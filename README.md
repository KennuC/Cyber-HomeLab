# PROJECTNAME

## Objective



### Skills Learned

- 

### Tools Used

- pfSense
- Kali Linux

## Steps


## Network Diagram

## Configuring pfSense

Create additional networks and vlans
add firewall rules for vlans for internet and vlan communication
DHCP for different networks

Create VLAN interfaces

![image](https://github.com/user-attachments/assets/0fc2b8b5-5b32-4684-bb15-b30fee783971)

Assign VLAN to LAN interface

![image](https://github.com/user-attachments/assets/0bd11398-7d59-4c53-826c-5a148f68a714)

Configure VLAN interfaces

VLAN10
![image](https://github.com/user-attachments/assets/69332e4b-345e-49c1-9a5e-87e16cf6905d)

VLAN20
![image](https://github.com/user-attachments/assets/93b3c940-4b2e-461a-8de2-345a86c56ba5)

VLAN30
![image](https://github.com/user-attachments/assets/62c8dec0-53b7-445e-b0ff-4de2fb6100b5)

Copy firewall rule of allow LAN to any from LAN to VLAN10,20,30. Also change source to appropriate subnet

![image](https://github.com/user-attachments/assets/af0c7608-9dc7-4885-9a24-7f9e6d32409d)

![image](https://github.com/user-attachments/assets/1c027a61-415b-44cd-9336-c8e026db58dc)

Enable DHCP server on each interface. Specify pool range and add DNS

![image](https://github.com/user-attachments/assets/2385db1b-123d-4c82-a62e-fe137d292a7f)

Install Docker on ubuntu server

![image](https://github.com/user-attachments/assets/bad0b8cf-373f-4084-afac-00755f17a396)

Install Portainer on ubuntu server

`sudo docker volume create portainer_data`

`sudo docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`

![image](https://github.com/user-attachments/assets/49fa2cfe-7622-4808-b8c5-5d1fb9310c8f)






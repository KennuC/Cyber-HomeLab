# PROJECTNAME

## Objective



### Skills Learned

- 

### Tools Used

- pfSense
- Kali Linux
- Ubuntu Server
- Docker
- Portainer
- bwapp
- dvwa
- webgoat
- Wazuh
- Nessus

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

## Configuring Docker and Portainer on ubuntu server

Install Docker on ubuntu server

![image](https://github.com/user-attachments/assets/bad0b8cf-373f-4084-afac-00755f17a396)

Install Portainer on ubuntu server

`sudo docker volume create portainer_data`  
`sudo docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`

![image](https://github.com/user-attachments/assets/49fa2cfe-7622-4808-b8c5-5d1fb9310c8f)

## Configure Macvlan in Portainer 

Under add network under networks tab. Configure VLAN30 config, add new network and select creation 

![image](https://github.com/user-attachments/assets/e958b277-042c-466e-865b-f550e40d355d)

![image](https://github.com/user-attachments/assets/f4499eec-4c36-40c5-9942-3c5463fcb4bc)

Create containers for bwapp, dvwa and web-goat making sure network is under `vlan30` and deploy.

![image](https://github.com/user-attachments/assets/f892c6b4-e9a6-440d-8006-ab2bd3b139bb)

## Wazuh

Using an Ubuntu Server, install Wazuh using  
`curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a`
Login using provided password and access the web page to confirm installation.  
![image](https://github.com/user-attachments/assets/c06bbbb7-5c4c-449e-906d-e4e9433d2368)

Deploying Wazuh agents on Linux endpoints.

Add the Wazuh repository

1. Install the GPG key: `curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg`
2. Add the repository:`echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list`
3. Update the package information:`apt-get update`
  
![image](https://github.com/user-attachments/assets/5de7517b-fe19-48b6-90f3-930927fb27b8)


Deploy a Wazuh agent on endpoint.  
`WAZUH_MANAGER="<IP>" apt-get install wazuh-agent`

Enable and start the Wazuh agent service.  
`systemctl daemon-reload`  
`systemctl enable wazuh-agent`  
`systemctl start wazuh-agent`  
![image](https://github.com/user-attachments/assets/b66f974d-5034-428f-aa6e-ed8bc076a87d)

Confirm agent status on Wazuh web interface.
![image](https://github.com/user-attachments/assets/8f4b238e-069f-4a4c-bf00-8596c7c8dbde)

Enable the Wazuh Docker listener to capture Docker events and forward them to the Wazuh server.    
`apt-get update && apt-get install python3`  
`apt-get install python3-pip`  
`pip3 install docker==4.2.0 urllib3==1.26.18`

Add the following configuration to the Wazuh agent configuration file /var/ossec/etc/ossec.conf to enable the Docker listener: 

```
<wodle name="docker-listener">
  <disabled>no</disabled>
</wodle>
```

Restart the Wazuh agent to apply the changes: `systemctl restart wazuh-agent`

Enable Wazuh Docker listener on dashboard  
![image](https://github.com/user-attachments/assets/1f5bc3e4-1011-4bc5-99aa-2c9d34e74df6)

Wazuh pfsense agent

Enable SSH in Settings > Advanced > Secure Shell > Enable Secure Shell



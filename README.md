# Cyber HomeLab

## Objective

### Skills Learned

### Tools Used

- Proxmox
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
- Caldera
- Security Onion
- Windows Server 2022
- Windows 10
- The Hive
- Cortex

## Network Diagram

![HomeLab drawio (3)](https://github.com/user-attachments/assets/bf878df6-e5e0-4935-9d7c-e012a1d8a11d)

## Troubleshooting



### Test 1

### Test 2 

## Setting up Proxmox 

### Storage

<img width="1058" height="522" alt="image" src="https://github.com/user-attachments/assets/e62b911b-c1ad-4182-8e61-5320ea46fe13" />

Set up SSD for VM (LVM-Thin)
pve > LVM-Thin > Create: Thinpool 

<img width="1065" height="525" alt="image" src="https://github.com/user-attachments/assets/df71573f-d17f-4f53-856b-bcf31ba9213d" />

Set up HDD for Other storage (ZFS)
pve > LVM-Thin > Create: ZFS

### Create a ZFS Dataset and Add it as a "Directory" Storage

<img width="242" height="175" alt="image" src="https://github.com/user-attachments/assets/4f258659-80c1-4954-8d3d-6b9e8f65d0ef" />

Promox shell 
For ISOs: `zfs create zfs-archive/iso-files`
For Container Templates: `zfs create zfs-archive/templates`
For Backups: `create zfs-archive/backups`

For each - Datacenter > Storage > Add > Directory > (ID) > (Directory - /zfs-archive/iso-files) > (Content).

### Network

Add Linux bridge 

pve > Network > Create > Linux Bridge > Apply Configuration
<img width="482" height="200" alt="image" src="https://github.com/user-attachments/assets/49e72cb2-65f2-4d39-8831-1284e881c75a" />

 
## pfSense

Create VM > Default settings

Hardware > Add > Network Device > vmbr2
<img width="477" height="211" alt="image" src="https://github.com/user-attachments/assets/1997d047-58b9-49dc-ad19-119178048552" />

Start > Console > Confirm/Next all > Reboot > N (Should VLANs be set up now?) > vtnet0 (WAN interface) > vtnet1 (LAN interface

<img width="318" height="62" alt="image" src="https://github.com/user-attachments/assets/f695e771-602b-4eeb-9e6b-b38cc2bd6954" />

2 (Set interface(s) IP address) > 2 (LAN) > N (LAN DHCP) > 10.10.1.254 (LAN IPv4) > 24 (subnet) > Enter (none) > N (IPv6) > Enter (none) > Y (Enable DHCP) > 10.10.1.50 - 10.10.1.100 > N (HTTP webConfigure protocol)

## Kali Build

Create VM > Storage: ssd-vm (120 GB) > 2 Cores > 8192 MiB > vmbr2 network bridge

Guided - use entire disk > All files in one partition > Yes Partition Disk > Yes GRUB boot loader > /dev/sda

Remove ISO

## pfSense Firewall Rules

Access pfSense @ 10.10.1.254 on web

### Networks

Interfaces > Assigments > VLANs

Add > vtnet1 - lan > VLAN 10 > Repeat for 20 & 30
<img width="1285" height="392" alt="image" src="https://github.com/user-attachments/assets/9e0d542a-4112-44cc-8703-ad4108206908" />

Interfaces > Assigments > Interface Assignments > Add VLAN 10, 20 & 30 > Save
<img width="1291" height="499" alt="image" src="https://github.com/user-attachments/assets/9f659fd7-2868-40d5-8d4d-2932d74b8f47" />







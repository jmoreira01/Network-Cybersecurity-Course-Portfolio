# Networking Basic Configuration
This project demonstrates the configuration of a Cisco 2911 router (RouterDoInferno) with three subnets (10.255.255.0/24, 172.31.255.0/24, 192.168.29.0/24) and DHCP for IP management. 
The network connects multiple PCs and a laptop via switches, as per the provided diagram.

## Notes
- All commands tested in a simulated environment in Cisco Packet Tracer.
- Future projects will include firewalls, VLANs, and traffic analysis.

**Files**: [Network Diagram](network_diagram.png)
```
> enable
> configure terminal
> line console 0
> login
> password MyPaSSwOrD
> exit
> enable secret MYeNABLEpAssWoRd
> service password-encryption
```

## Network Overview

**Router**: RouterDoInferno (Cisco 2911)
**Interfaces**:
- GigabitEthernet0/0: 10.255.255.1/24 (to Fa0/5 switch)
- GigabitEthernet0/1: 172.31.255.1/24 (to Fa0/4 switch)
- GigabitEthernet0/2: 192.168.29.1/24 (to Fa0/3 switch)

**Devices**: PCs (PC1 to PC12) and Laptop-PT across switches.
**Diagram Reference**: Star topology with router at center.

## Step-by-Step Configuration
```
> enable - Access Privileged EXEC mode.
> configure terminal - Enter Global Configuration mode.
> hostname RouterDoInferno - Rename the device.
> line console 0 - Configure console login.
    login
    password MyConsolePassword
    exit
```
## Configure first subnet
```
> enable secret MYEnablePassword - Set Privileged EXEC password.
> service password-encryption - Encrypt passwords.
> interface GigabitEthernet0/0 - Configure first subnet.
    ip address 10.255.255.1 255.255.255.0
    no shutdown
    exit
```
## Set up DHCP for 10.255.255.0/24 - "ESQUERDA"
```
> ip dhcp pool Esquerda - Set up DHCP for 10.255.255.0/24.
    > network 10.255.255.0 255.255.255.0
    > default-router 10.255.255.1
    > exit
```
## Configure second subnet
```
> interface GigabitEthernet0/1 - Configure second subnet.
  > ip address 172.31.255.1 255.255.255.0
  > no shutdown
  > exit
```
## Set up DHCP for 10.255.255.0/24 - "MEIO"
```
> ip dhcp pool Meio - Set up DHCP for 172.31.255.0/24.
  > network 172.31.255.0 255.255.255.0
  > default-router 172.31.255.1
  > exit
```
## Configure third subnet
```
> interface GigabitEthernet0/2 - Configure third subnet.
  > ip address 192.168.29.1 255.255.255.0
  > no shutdown
  > exit
```
## Set up DHCP for 10.255.255.0/24 - "DIREITA"
```
> ip dhcp pool Direita - Set up DHCP for 192.168.29.0/24.
  > network 192.168.29.0 255.255.255.0
  > default-router 192.168.29.1
  > exit
```
## Banner config
```
> banner motd # 
  > " THIS IS A CONSOLE BANNER #" - Add banner
```

## Checking configuration 
```
show running-config - Verify configuration.
```

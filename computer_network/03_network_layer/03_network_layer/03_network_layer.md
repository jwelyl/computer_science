# Network Layer(L3)

# IPv4

- **32bit address**
- **Host를 식별함**
- **Network ID (24bit) + Host ID(8bit)**

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%201.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%202.png)

# Packet, Maximum Transmission Unit (MTU)

- **Network Layer(L3)에서의 단위 데이터가 Packet임**
    
    Datalink Layer(L2)에서는 Frame, Transport Layer(L4)에서는 Segment
    
- **Paket은 Header와 Payload로 나뉨**
    - Header : src IP address, dst IP address 포함 20bytes
    - Payload : 1,480bytes
- **Packet의 최대 크기는 MTU로 1,500bytes임**

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%203.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%204.png)

# Encapsulation/Decapsulation

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%205.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%206.png)

# Packet Lifecycle

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%207.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%208.png)

# Protocol Data Unit (PDU)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%209.png)

[Protocol Data Unit (PDU) - GeeksforGeeks](https://www.geeksforgeeks.org/protocol-data-unit-pdu/)

# TCP/IP Structure

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2010.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2011.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2012.png)

# IPv4 Header

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2013.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2014.png)

# Subnet Mask, CIDR

## Subnet Mask

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2015.png)

## Classless Inter-Domain Routing (CIDR)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2016.png)

# Broadcast IP Address

**32bit IPv4 Address 중 마지막 8bit가 모두 1일 경우, 즉 xxx.xxx.xxx.255일 경우, Broadcast IP이다.**

48bit MAC Address 모든 bit가 1일 경우, 즉 FF-FF-FF-FF-FF-FF일 경우, Broadcast MAC Address이다.

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2017.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2018.png)

# Loopback  IP Address

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2019.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2020.png)

# Internet, Router

## Internet

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2021.png)

## TTL, Fragmentation

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2022.png)

![fragmentation.png](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/fragmentation.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2023.png)

# DHCP

## Internet Configuration

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2024.png)

## Dynamic Host Configuration Protocol (DHCP)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2025.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2026.png)

# Address Resolution Protocol (ARP)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2027.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2028.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2029.png)

# Ping, RTT

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2030.png)

![Untitled](Network%20Layer(L3)%20653ec6e197c24a2ea94dbe55b6ba109e/Untitled%2031.png)
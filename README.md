# intervlan-routing-project
Inter-VLAN routing using router-on-a-stick

## 🎯 Objective
1. Build the Network and Configure Basic Device Settings
2. Create VLANs and Assign switch ports
3. Configure 802.1Q Trunk between the Switches
4. Configure Inter-VLAN routing on the Router
5. Verify if the Inter-Vlan is working

## 🧠 Concept Use
1. VLANs
2. Trunking
3. Inter-VLAN routing

## Tools
1. Cisco Packet Tracer

## Topology
1. Logical Topology

## Router Configuration

enable secret class

line console 0
password cisco
login
exit

line vty 0 4
password cisco
login
exit

service password-encryption

banner motd# Unauthorized Access is Prohibited!#

clock set 14:30:00 March 22, 2026

configure terminal
int g0/0/1
no shutdown

int g0/0/1.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

int g0/0/1.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0
no shutdown
exit

int g0/0/1.30
encapsulation dot1q 30
ip address 192.168.30.1 255.255.255.0
no shutdown
exit

int g0/0/1.1000

## Switch Configurations

int vlan 10
ip address 192.168.10.11 255.255.255.0
no shutdown
exit

ip default-gateway 192.168.10.1

#VLANs Configurations
configure terminal
vlan 10 
name Management

vlan 20
name Sales

vlan 30
name Operations

vlan 999
name Parking_Lot

vlan 1000
native VLAN

#Interface assigning ports
configure terminal
int f0/6      
switchport mode access
switchport access vlan 20
no shutdown 
exit

int range f0/2-4
switchport mode access
switchport access vlan 999
shutdown

int range f0/7-24
switchport mode access
switchport access vlan 999
shutdown

int range g0/1-2
switchport mode access
switchport access vlan 999
shutdown

int f0/18
switchport mode access
switchport access vlan 30
no shutdown
exit

int range f0/2-17
switchport mode access
switchport access vlan 999
shutdwon

int range f0/19-24
switchport mode access
switchport access vlan 999
shutdwon

int range g0/1-2
switchport mode access
switchport access vlan 999
shutdown

#Set up Trunk
configure terminal
int f0/1
switchport mode trunk
switchport trunk native vlan 1000
switchport trunk allowed 10,20,30,1000
exit


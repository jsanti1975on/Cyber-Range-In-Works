# Full Configuration Checklist: Cisco Switches and RV340 for VLAN 10 Trunking

---

## 1. General Preparation

### Access the Switch (via Console or SSH)
1. Log in to the switch.
2. Enter privileged EXEC mode:
   ```plaintext
   Switch> enable
   ```
3. Enter global configuration mode:
   ```plaintext
   Switch# configure terminal
   ```

---

## 2. Configure Switch 1 (East)

### A. Basic Configuration
1. Set hostname:
   ```plaintext
   Switch(config)# hostname East
   ```
2. Disable DNS lookup:
   ```plaintext
   East(config)# no ip domain-lookup
   ```
3. Enable IP routing:
   ```plaintext
   East(config)# ip routing
   ```

### B. VLAN Configuration
1. Create VLAN 10 and name it "Server":
   ```plaintext
   East(config)# vlan 10
   East(config-vlan)# name Server
   East(config-vlan)# exit
   ```
2. Assign IP address to VLAN 10 interface:
   ```plaintext
   East(config)# interface vlan 10
   East(config-if)# ip address 172.20.10.1 255.255.255.0
   East(config-if)# no shutdown
   East(config-if)# exit
   ```

### C. Configure Trunk for Backbone (to Switch 2)
1. Configure `GigabitEthernet0/1` as a trunk port:
   ```plaintext
   East(config)# interface GigabitEthernet0/1
   East(config-if)# switchport mode trunk
   East(config-if)# switchp

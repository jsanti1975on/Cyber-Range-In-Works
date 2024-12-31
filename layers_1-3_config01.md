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
   East(config-if)# switchport trunk encapsulation dot1q
   East(config-if)# switchport trunk allowed vlan 10
   East(config-if)# description Backbone to West
   East(config-if)# exit
   ```

### D. Configure Trunk for Cisco RV340
1. Configure `FastEthernet0/8` as a trunk to the RV340:
   ```plaintext
   East(config)# interface FastEthernet0/8
   East(config-if)# switchport mode trunk
   East(config-if)# switchport trunk encapsulation dot1q
   East(config-if)# switchport trunk allowed vlan 10
   East(config-if)# description Trunk to Cisco RV340
   East(config-if)# exit
   ```

### E. Save the Configuration
1. Save the configuration to prevent loss:
   ```plaintext
   East# write memory
   ```

---

## 3. Configure Switch 2 (West)

### A. Basic Configuration
1. Set hostname:
   ```plaintext
   Switch(config)# hostname West
   ```
2. Disable DNS lookup:
   ```plaintext
   West(config)# no ip domain-lookup
   ```
3. Enable IP routing:
   ```plaintext
   West(config)# ip routing
   ```

### B. VLAN Configuration
1. Create VLAN 10 and name it "Server":
   ```plaintext
   West(config)# vlan 10
   West(config-vlan)# name Server
   West(config-vlan)# exit
   ```
2. Assign IP address to VLAN 10 interface:
   ```plaintext
   West(config)# interface vlan 10
   West(config-if)# ip address 172.20.10.2 255.255.255.0
   West(config-if)# no shutdown
   West(config-if)# exit
   ```

### C. Configure Trunk for Backbone (to Switch 1)
1. Configure `GigabitEthernet0/1` as a trunk port:
   ```plaintext
   West(config)# interface GigabitEthernet0/1
   West(config-if)# switchport mode trunk
   West(config-if)# switchport trunk encapsulation dot1q
   West(config-if)# switchport trunk allowed vlan 10
   West(config-if)# description Backbone to East
   West(config-if)# exit
   ```

### D. Save the Configuration
1. Save the configuration to prevent loss:
   ```plaintext
   West# write memory
   ```

---

## 4. Configure the Cisco RV340

1. Log in to the Cisco RV340 web interface.
2. Navigate to **LAN > VLAN Settings**.
3. Create VLAN 10:
   - VLAN ID: `10`
   - Name: `Server`
4. Assign an IP address to VLAN 10:
   - Example: `172.20.10.254/24`
5. Save and apply the configuration.

---

## 5. Test and Verify Configuration

### A. On Both Switches

1. Verify VLAN configuration:
   ```plaintext
   Switch# show vlan brief
   ```
   - Ensure VLAN 10 is created and named "Server."

2. Verify trunk configuration:
   ```plaintext
   Switch# show interfaces trunk
   ```
   - Confirm `GigabitEthernet0/1` and `FastEthernet0/8` are in trunk mode.

3. Verify IP interface configuration:
   ```plaintext
   Switch# show ip interface brief
   ```

### B. Connectivity Testing

1. From Switch 1 (East), ping Switch 2 (West):
   ```plaintext
   East# ping 172.20.10.2
   ```

2. From Switch 1 (East), ping the Cisco RV340 gateway:
   ```plaintext
   East# ping 172.20.10.254
   ```

3. From Switch 2 (West), ping the Cisco RV340 gateway:
   ```plaintext
   West# ping 172.20.10.254
   ```

4. Connect a device on VLAN 10 to verify end-to-end connectivity.

---

## Checklist Summary

1. **Switch 1 (East)**:
   - VLAN 10 configured.
   - Trunk on `G0/1` to Switch 2.
   - Trunk on `F0/8` to RV340.

2. **Switch 2 (West)**:
   - VLAN 10 configured.
   - Trunk on `G0/1` to Switch 1.

3. **Cisco RV340**:
   - VLAN 10 configured with IP `172.20.10.254/24`.

---

This checklist ensures the switches and router are correctly configured for VLAN 10 trunking and backbone connectivity.

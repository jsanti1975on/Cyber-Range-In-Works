# Checklist: Configure a Trunk Between Cisco Switch and Cisco RV340

## 1. Prepare the Switch Configuration

### Access the Switch via Console or SSH
1. Log in to the switch.
2. Enter privileged EXEC mode:
   ```plaintext
   Switch> enable
   ```
3. Enter global configuration mode:
   ```plaintext
   Switch# configure terminal
   ```

### Create VLAN 10 and Name It "Server"
1. Add VLAN 10:
   ```plaintext
   Switch(config)# vlan 10
   ```
2. Name VLAN 10 as "Server":
   ```plaintext
   Switch(config-vlan)# name Server
   ```
3. Exit VLAN configuration:
   ```plaintext
   Switch(config-vlan)# exit
   ```

### Configure FastEthernet0/8 as a Trunk Port
1. Enter interface configuration for FastEthernet0/8:
   ```plaintext
   Switch(config)# interface FastEthernet0/8
   ```
2. Set the port to trunk mode:
   ```plaintext
   Switch(config-if)# switchport mode trunk
   ```
3. Configure the trunk encapsulation (if required):
   ```plaintext
   Switch(config-if)# switchport trunk encapsulation dot1q
   ```
4. Allow only VLAN 10 on the trunk:
   ```plaintext
   Switch(config-if)# switchport trunk allowed vlan 10
   ```
5. Exit interface configuration mode:
   ```plaintext
   Switch(config-if)# exit
   ```

### Save the Configuration
1. Save the running configuration to startup:
   ```plaintext
   Switch# write memory
   ```

### Verify the Configuration
1. Check VLANs:
   ```plaintext
   Switch# show vlan brief
   ```
   - Confirm VLAN 10 is listed as "Server."
2. Verify trunk configuration:
   ```plaintext
   Switch# show interfaces trunk
   ```
   - Confirm FastEthernet0/8 is in trunk mode and allows VLAN 10.

---

## 2. Prepare the Cisco RV340 Configuration

### Log in to the Cisco RV340 via the Web GUI
1. Access the router’s web interface using its IP address.
2. Log in with your administrator credentials.

### Create VLAN 10
1. Navigate to **LAN > VLAN Settings**.
2. Add VLAN ID 10.
3. Name the VLAN (e.g., "Server").

### Assign an IP Address to VLAN 10
1. Configure the VLAN 10 IP settings:
   - Example: `172.20.10.254/24`.

### Save and Apply the Configuration
1. Save the changes to ensure the configuration is active.

---

## 3. Test the Configuration

### Test Ping Between the Switch and RV340
1. From the switch, ping the RV340 VLAN 10 IP address:
   ```plaintext
   Switch# ping 172.20.10.254
   ```

### Verify VLAN 10 Connectivity
1. Connect a device to VLAN 10 on the switch.
2. Test connectivity to the RV340 VLAN 10 gateway (`172.20.10.254`).

---

## 4. Troubleshooting (If Needed)
1. Verify VLAN configuration on the switch:
   ```plaintext
   Switch# show vlan brief
   ```
2. Verify trunk settings:
   ```plaintext
   Switch# show interfaces trunk
   ```
3. Check if the VLAN 10 interface on the RV340 is active.
4. Check physical connections between the switch and router.

---

## Checklist Complete
- **VLAN 10** is configured and named "Server."
- **FastEthernet0/8** is a trunk port allowing VLAN 10.
- **RV340** is configured for VLAN 10 with IP settings.
- Devices on VLAN 10 can communicate with the RV340 gateway.

---

This checklist ensures consistency and ease of repeating the configuration process.

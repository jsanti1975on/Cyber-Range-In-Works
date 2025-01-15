# Setting a Default IP Route on a Specific Network Interface in Debian/Ubuntu

## 1. Check the Existing Routing Table

To view the current routing table, use the following command:

```bash
ip route show
```
## Delete the Current Default Route (if necessary)

```bash
sudo ip route del default
```

## Add a New Default Route

```bash
sudo ip route add default via <gateway-ip> dev <interface>
```

## Verify the Routing Table

```bash
ip route show
```

## Make the Default Route Persistent => {^_^}LOOKEY_FLAG No persistant route until esxi-west is at the point in the RHEL course Spring semester 2025

The above changes will only last until the next reboot. To make the default route persistent, you need to modify the appropriate network configuration files based on your system's configuration.

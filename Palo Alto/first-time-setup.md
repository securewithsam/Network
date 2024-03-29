#### Setting up PA-220 

## If you dont know the password:
As the firewall is booting up, type "maint" into CLI via console port and then you can choose the option: Reset to Factory Default.

### Step 1: Login to CLI and setup MGMT IP
```sh

set deviceconfig system ip-address 192.168.220.200
set deviceconfig system netmask 255.255.255.0
set deviceconfig system default-gateway 192.168.220.1
set deviceconfig system dns-setting servers primary 8.8.8.8
```


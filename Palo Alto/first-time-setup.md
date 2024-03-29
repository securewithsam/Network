### Setting up PA-220 

#### If you dont know the password:
As the firewall is booting up, type "maint" into CLI via console port and then you can choose the option: Reset to Factory Default.

#### Step 1: Login to CLI and setup MGMT IP
```sh

set deviceconfig system ip-address 10.0.100.220
set deviceconfig system netmask 255.255.255.0
set deviceconfig system default-gateway 10.0.100.220.1
set deviceconfig system dns-setting servers primary 8.8.8.8
```
![1](https://github.com/securewithsam/Network/assets/85324643/9226d272-5058-4152-9eae-77b01ea54b2a)

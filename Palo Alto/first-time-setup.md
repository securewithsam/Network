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
```sh
set mgt-config users admin password
```
![1](https://github.com/securewithsam/Network/assets/85324643/9226d272-5058-4152-9eae-77b01ea54b2a)
![2](https://github.com/securewithsam/Network/assets/85324643/06f87758-256e-4b3c-86a0-771170a5af16)

### Step2: Configuring Interfaces
WAN is on interface ethernet1/8 and the LAN on interface ethernet1/3

![3](https://github.com/securewithsam/Network/assets/85324643/6b56f710-1d1f-438f-8634-872ed9debc07)

![4](https://github.com/securewithsam/Network/assets/85324643/b12d2091-ddc0-4588-baeb-8fdfad1dc23a)

![8](https://github.com/securewithsam/Network/assets/85324643/20d8bb8a-4f2d-4669-8708-6b4f84c1ffb5)

![7](https://github.com/securewithsam/Network/assets/85324643/062596a5-a95f-4d10-8e73-f011e7684980)


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
```sh
commit
```
![1](https://github.com/securewithsam/Network/assets/85324643/9226d272-5058-4152-9eae-77b01ea54b2a)
![2](https://github.com/securewithsam/Network/assets/85324643/06f87758-256e-4b3c-86a0-771170a5af16)

### Step2: Configuring Interfaces
WAN is on interface ethernet1/8 and the LAN on interface ethernet1/3

WAN -ISP
![3](https://github.com/securewithsam/Network/assets/85324643/6b56f710-1d1f-438f-8634-872ed9debc07)

![4](https://github.com/securewithsam/Network/assets/85324643/b12d2091-ddc0-4588-baeb-8fdfad1dc23a)

LAN 
![8](https://github.com/securewithsam/Network/assets/85324643/20d8bb8a-4f2d-4669-8708-6b4f84c1ffb5)

![9](https://github.com/securewithsam/Network/assets/85324643/f73c5096-c1b3-40f0-a9b5-ac1e155c6cd0)

#### Step3: Configure Zones

![10](https://github.com/securewithsam/Network/assets/85324643/b7d6b081-f286-4a08-ae32-8de5d9d9127b)
![11](https://github.com/securewithsam/Network/assets/85324643/70bc2a0a-5295-4d07-a746-d3753b19d634)

#### Step 4: Configure DHCP

![12](https://github.com/securewithsam/Network/assets/85324643/6e8cd14f-6877-4169-b0da-3920ea39464e)

![13](https://github.com/securewithsam/Network/assets/85324643/c3e35562-44f5-40ba-ba48-c019663f4fdc)

#### Step 5:  NAT

![15](https://github.com/securewithsam/Network/assets/85324643/954421eb-2f67-4c8e-9b27-73fdf33d8615)

![16](https://github.com/securewithsam/Network/assets/85324643/1dcbcf6a-adb5-4e7e-af8b-31ae66cb9f78)

![17](https://github.com/securewithsam/Network/assets/85324643/55ec4d09-98ca-43aa-91e7-bea5c1b6fd32)

#### Step 6: Routes

![18](https://github.com/securewithsam/Network/assets/85324643/b5373b30-187d-4354-bab2-657128ac3339)

![19](https://github.com/securewithsam/Network/assets/85324643/684ee6eb-f75b-48f8-a6d9-ec176d722684)


#### Step 7:  Commit

![14](https://github.com/securewithsam/Network/assets/85324643/0bc621bf-ab6e-411b-9c2f-c78882e611aa)


## At this time you should have internet 


## VLAN CONFIGURATION 

![image](https://github.com/securewithsam/Network/assets/85324643/0d590628-50aa-49dd-abb4-e90504f214d2)

![image](https://github.com/securewithsam/Network/assets/85324643/462e7203-c78b-4eb2-b4af-de05efb98575)

![image](https://github.com/securewithsam/Network/assets/85324643/d71d00fc-00c1-4917-8512-445a1c371a88)

![image](https://github.com/securewithsam/Network/assets/85324643/d43638c0-020f-4bc2-bf24-94a99a90a70a)

![image](https://github.com/securewithsam/Network/assets/85324643/8bef59ae-1088-4615-901b-b8660a0287ab)

![image](https://github.com/securewithsam/Network/assets/85324643/18a135d9-fd87-4ac6-9782-de9aae9cb730)

![image](https://github.com/securewithsam/Network/assets/85324643/af50a6ad-bea3-47a1-bde3-cad0240229d7)

![image](https://github.com/securewithsam/Network/assets/85324643/056ff2ad-a9c4-49a5-85bd-024cbfa916bd)















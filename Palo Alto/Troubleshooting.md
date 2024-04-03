#### https://docs.paloaltonetworks.com/pan-os/9-1/pan-os-cli-quick-start/cli-cheat-sheets

#### To check leds
```sh
show system state filter chassis.leds
```
#### check fan and psu
```sh
show system environmentals 
```
#### To check interface
```sh
show interface ethernet1/1 | match link
```
show log system query equal "( eventid eq link-change ) and ( object eq 'ethernet1/1' )" direction equal backward     (To check interface flapping /up and down)


APP-ID | Vulnerability Profile | Antivirus Profile are L7 and perform DPI (deep packet inspection) and will use full resources.

#### How to check sessions or throughput : Match againts the datasheet for the model#
```sh
show session info
show counter global filter severity warn delta yes
show running resource-monitor second ( to review dataplane CPU usage)
show running resource-monitor ingress-backlogs
```


#### To check if a policy is working or not :
```sh
test security-policy-match source 10.1.1.1 destination 200.1.1.1 protocol 1
test routing fib-lookup virtual-router default ip 200.1.1.1
Debug Dataplane packet-diag set filter match source 10.1.1.1 destination 200.1.1.1 
Debug Dataplane packet-diag set filter on
show counter global filter packet-filter yes severity drop
```
(then test the policy or tyr to ping and chk the debug for more info)


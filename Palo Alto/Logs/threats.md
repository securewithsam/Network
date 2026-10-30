
### Attempted attacks (everything, blocked or not)
```sh
( severity geq high ) and ( ( zone.src eq UNTRUST-INTERNET ) or ( zone.dst eq UNTRUST-INTERNET ) ) and ( ( subtype eq vulnerability ) or ( subtype eq spyware ) or ( subtype eq virus ) or ( subtype eq wildfire-virus ) )
```

### Brute-force attempts blocked (HTTP, SSH, RDP password-guessing and so on)

```sh
( severity geq high ) and ( ( zone.src eq UNTRUST-INTERNET ) or ( zone.dst eq UNTRUST-INTERNET ) ) and ( category-of-threatid eq brute-force ) and ( action neq alert ) and ( action neq allow )
```

### Exploit attempts blocked (vulnerability attacks, excluding brute force)

```sh
( severity geq high ) and ( ( zone.src eq UNTRUST-INTERNET ) or ( zone.dst eq UNTRUST-INTERNET ) ) and ( subtype eq vulnerability ) and ( category-of-threatid neq brute-force ) and ( action neq alert ) and ( action neq allow )
```

### Malware/spyware blocked

```sh
( severity geq high ) and ( ( zone.src eq UNTRUST-INTERNET ) or ( zone.dst eq UNTRUST-INTERNET ) ) and ( ( subtype eq virus ) or ( subtype eq wildfire-virus ) or ( subtype eq spyware ) ) and ( action neq alert ) and ( action neq allow )

```

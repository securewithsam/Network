# Internet Threats (High/Critical): Palo Alto Threat Log Query

A PAN-OS / Panorama threat log filter that returns every **high or critical severity threat** detected in traffic **between the internal network and the internet, in both directions**.

It is designed as the data source for an executive cyber posture report: how much malicious activity the firewall saw, how much it stopped, and what got through.

**Suggested saved filter name:** `ELT-Internet-Threats-High-Critical`

---

## The Query

```
( ( zone.src eq UNTRUST-INTERNET ) or ( zone.dst eq UNTRUST-INTERNET ) ) and ( severity geq high ) and ( ( subtype eq vulnerability ) or ( subtype eq spyware ) or ( subtype eq virus ) or ( subtype eq wildfire-virus ) )
```

> Replace `UNTRUST-INTERNET` with the name of your internet-facing zone. Zone names are case-sensitive and must match exactly what appears in the **Source Zone** / **Destination Zone** columns of your logs.

---

## How It Works

The query has three conditions joined by `and`. A log entry must match all three.

### 1. Traffic touching the internet

```
( ( zone.src eq UNTRUST-INTERNET ) or ( zone.dst eq UNTRUST-INTERNET ) )
```

| Condition | Meaning |
|---|---|
| `zone.src eq UNTRUST-INTERNET` | Traffic that came **from** the internet (inbound) |
| `zone.dst eq UNTRUST-INTERNET` | Traffic going **to** the internet (outbound, initiated by internal users or systems) |

Internal-only traffic (for example, server to server) is excluded.

### 2. Serious threats only

```
( severity geq high )
```

`geq` means greater than or equal to. This keeps **High** and **Critical** only. Low, medium and informational detections are excluded because they are mostly noise at executive level.

### 3. Real threat types only

```
( ( subtype eq vulnerability ) or ( subtype eq spyware ) or ( subtype eq virus ) or ( subtype eq wildfire-virus ) )
```

| Subtype | Plain-language meaning |
|---|---|
| `vulnerability` | An attempt to exploit a software weakness, such as a malicious website attacking a browser or a scanner probing a server |
| `spyware` | A device communicating with a known attacker-controlled (command and control) server, or traffic matching known spyware behaviour |
| `virus` | A known malicious file crossing the firewall, usually a download |
| `wildfire-virus` | A file that the WildFire sandbox determined to be malware, including new malware with no prior signature |

Excluded on purpose: URL filtering, file blocking and data filtering matches. These are policy enforcement, not attacks.

---

## Reading the Results

### Action column

| Action | Meaning |
|---|---|
| `reset-both`, `reset-client`, `reset-server`, `drop`, `deny`, `block-ip`, `sinkhole` | **Blocked** |
| `alert`, `allow` | **Detected but not stopped.** Review these. |

### Repeat Count column

The firewall aggregates identical threats between the same source and destination into one log entry. **Sum the Repeat Count column for true volume. Do not count rows.** One row can represent thousands of events.

### Deriving report metrics

| Metric | How to calculate |
|---|---|
| **Attempted / detected** | Sum of Repeat Count across all rows |
| **Blocked** | Sum of Repeat Count where Action is not `alert` or `allow` |
| **Got past controls** | Sum of Repeat Count where Action is `alert` or `allow` |
| **Blocked %** | Blocked ÷ Attempted |

"Got past controls" should be at or near zero. If it is not, a security profile is likely set to `alert` where it should be blocking. That is a configuration finding in its own right.

---

## Important Interpretation Notes

### Outbound spyware is not just "blocked"

A `spyware` detection where the **source is an internal host** usually means a device attempted to contact a command and control server or hit a DNS sinkhole. Even when blocked, this suggests the device **may already be compromised**.

Treat these as **under investigation**, not as a control success, and check the host in your EDR.

Companion query for these events:

```
( zone.dst eq UNTRUST-INTERNET ) and ( subtype eq spyware ) and ( severity geq high )
```

Suggested name: `ELT-Internal-C2-Callouts-High-Critical`

### Few or no inbound results is normal

Threat inspection only runs on traffic a security rule has already allowed. If few services are published inbound through the firewall, internet scanning is dropped by policy **before** threat inspection, so it never generates threat logs. In that case most results will be outbound, and the metric effectively answers:

> "Is malicious internet content reaching our users and systems?"

rather than "Are attackers breaking in?" Label your reporting accordingly.

### Do not use traffic log denies as "attacks blocked"

Traffic log denies include every packet dropped by default-deny policy, mostly background internet scanning. The number is very large and not meaningful as a risk indicator. Threat logs are the better measure of attempted attacks.

---

## Usage

1. Go to **Monitor > Logs > Threat** (firewall or Panorama).
2. In Panorama, set the **Device** context to Panorama (all devices) unless you want a single firewall.
3. Paste the query into the filter bar.
4. Set the time range (for example, **Last 7 Days**) and click **Apply Filter**.
5. Save the filter for reuse.
6. Export to CSV from the top right of the log table if needed.

### Automating daily counts

The log viewer shows entries, not totals. For a daily number, create a scheduled custom report:

- **Monitor > Manage Custom Reports** (wording varies slightly by version)
- **Database:** Threat Summary
- **Time frame:** Last Calendar Day
- **Group by:** Action, with the Count column included
- **Query:** paste the filter above
- **Schedule:** enabled, delivered via an email scheduler or report group

---

## Troubleshooting a Blank Result

Build the filter up one condition at a time. Whichever step returns nothing is the problem.

| Step | Filter | If blank |
|---|---|---|
| 1 | *(empty filter)* | No threat logs reaching this device, or wrong Panorama context |
| 2 | `( severity geq high )` | No high/critical threats in range. Try `( severity geq medium )` |
| 3 | `( severity geq high ) and ( zone.dst eq <ZONE> )` | Zone name mismatch. Copy it exactly from a log row |
| 4 | Full query | A subtype condition is excluding everything |

You can also build the filter with the **+ (Add Filter)** button to get syntax that matches your PAN-OS version.

---

## Exporting and Data Handling

- **Row limits:** Panorama caps CSV exports (the *Max Rows in CSV Export* setting). If your export row count sits exactly at the cap, the data has been truncated and your totals will be understated.
- **Sensitive content:** Raw threat logs contain internal IP addresses, zone names, hostnames and which systems were targeted. Only process exports in tools approved by your organization, and strip source and destination IP columns before sharing outside the security team.
- **Executive reporting:** Report aggregates only. Never include hostnames, IPs, usernames or vulnerability details in material that may be forwarded.

---

## Compatibility

Written for PAN-OS / Panorama log filter syntax. Strata Cloud Manager and Prisma Access log viewers use a different query syntax and will need adaptation.

# Home Security Operations Center (SOC) Lab

This document highlights a **Home Security Operations Center (SOC) Lab** I completed, showcasing my experience in building and analyzing a cloud-based security monitoring solution using Microsoft Sentinel. This project demonstrates my skills in configuring security infrastructure, analyzing threats, and leveraging SIEM tools for incident detection.

---
### Lab Overview and Architecture

![Screenshot_17-2-2025_175758_www youtube com](https://github.com/user-attachments/assets/0a461ed4-bfb6-41ce-a559-f5094e10a9c4)

- **Azure Resource Group:** Central hub for services.
- **Virtual Network (VNet):** Secure network environment.
- **Windows 10 Virtual Machine (Honeypot):** Publicly exposed to attract attackers.
- **Network Security Group (NSG):** Configured to allow all traffic.
- **Log Analytics Workspace:** Collects and stores security event logs.
- **Azure Monitoring Agent:** Forwards security logs to Sentinel.
- **Microsoft Sentinel:** Analyzes logs and visualizes attack patterns.

---
### Key Concepts Covered
- **SIEM and Threat Analysis:** Real-time log monitoring and incident detection.
- **KQL Queries:** Queried logs to identify attack trends and failed logins.
- **Geolocation Tracking:** Used watchlists to track attacker locations.
- **Honeypot Configuration:** Analyzed real, live, attacks on exposed services.

---
### Step-by-Step Instructions
**1. Environment Setup:**
   - Created an Azure Resource Group and VNet.
   - Deployed a Windows 10 Virtual Machine (honeypot) in the VNet.
   - Configured an NSG to allow all traffic and disabled Windows Firewall.

**2. Log Collection Configuration:**
   - Set up a Log Analytics Workspace.
   - Installed the Azure Monitoring Agent on the honeypot.
   - Configured the agent to forward security logs (Event ID 4625 - Failed Logons).

**3. Sentinel Integration:**
   - Connected Microsoft Sentinel to the Log Analytics Workspace.
   - Uploaded a watchlist with geolocation data (IP blocks by region).

![Screenshot_17-2-2025_175729_drive google com](https://github.com/user-attachments/assets/2426fbfd-73de-4978-abcc-11b828466ef9)

**4. Attack Monitoring with KQL:**
   - Ran KQL queries to identify failed logon attempts and cross-referenced with the watchlist.
   - Visualized attack origins on a world map using Sentinel workbooks.

**Example KQL Query:**
```kql
let GeoIPDB_FULL = _GetWatchlist("geoip");
let WindowsEvents = SecurityEvent
    | where IpAddress == <attacker IP address>
    | where EventID == 4625
    | order by TimeGenerated desc
    | evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network);
WindowsEvents
```

**5. Results and Visualization:**
   - Displayed attack patterns on Sentinel workbooks.
   - Analyzed trends over time to identify targeted attack attempts.

![Screenshot_17-2-2025_17577_portal azure com](https://github.com/user-attachments/assets/ca337920-3062-49af-8071-670de57b47de)

---
### Outcomes and Skills Gained
- **Practical SIEM experience:** Proficient in using Microsoft Sentinel and KQL.
- **Threat Analysis:** Identified and visualized attack sources from real-world traffic.
- **Honeypot Management:** Simulated and detected attack scenarios effectively.

### Future Enhancements
- Develop custom detection rules for SSH brute force attempts.
- Implement automated response playbooks.
- Expand the setup with multiple honeypot VMs.

---
This project reflects my hands-on experience in security operations, log analysis, and SIEM workflows, making me well-prepared for security analyst roles.

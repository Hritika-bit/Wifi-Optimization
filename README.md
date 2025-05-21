## Wifi-Optimization
# Home Network Configuration Project

As part of my self-learning journey into **network engineering**, I recently configured a dual-router setup using a **Huawei ONT Router** and a **LB-Link Router** to enhance signal strength, optimize internet speed, and enable seamless device connectivity.

### Key Accomplishments

- Set up a **LAN-to-LAN bridge** between the routers to allow better coverage while avoiding IP conflicts.
- Assigned a **static IP** to the Huawei router within the subnet managed by the LB-Link router.
- Disabled DHCP on the Huawei router and enabled it on the LB-Link to centralize IP allocation.
- Merged **2.4 GHz and 5 GHz bands** under a unified SSID for better signal handoff and device roaming.
- Adjusted advanced wireless settings including **channel width, transmission power, and beacon intervals**.
- Verified performance via `speedtest-cli` and system diagnostics:
  - **Ping:** ~29 ms  
  - **Download:** ~5.37 Mbps  
  - **Upload:** ~5.23 Mbps  

This setup significantly improved the network’s **coverage**, **stability**, and **device response time**.

---

### Network Topology Diagram

```mermaid
graph TD
    Internet((Internet)) --> ONU[Huawei ONT Router<br/>Static IP<br/>DHCP Disabled<br/>AP Mode<br/>2nd Floor Coverage]
    ONU --> LBL[LB-Link Router<br/>DHCP Enabled<br/>Primary Router<br/>1st Floor Coverage]
    
    subgraph "2nd Floor Devices"
        ONU --> Phone2[Smartphones]
        ONU --> Laptop2[Laptops]
        ONU --> OtherDevices2[Other Devices]
    end
    
    subgraph "1st Floor Devices"
        LBL --> Phone1[Smartphones]
        LBL --> Laptop1[Laptops]
        LBL --> SmartTV[Smart TV]
        LBL --> OtherDevices1[Other Devices]
    end
    
    classDef router fill:#f9f,stroke:#333,stroke-width:2px;
    class ONU,LBL router;
    
    Admin[Admin Users] --> FW
    Developers[Developers] --> FW
    CITools[External CI Tools] --> FW
```

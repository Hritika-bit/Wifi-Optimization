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

graph TD
    subgraph "Internet / External Access"
        Internet((Internet)) --> FW[Load Balancers<br/>& Firewalls]
    end
    
    subgraph "GitHub Edge Network"
        FW --> CDN[CDN Edge Cache]
        FW --> DDoS[DDoS Protection]
        CDN --> API[API Gateway]
        DDoS --> API
    end
    
    subgraph "GitHub Core Services"
        API --> Auth[Authentication<br/>Services]
        API --> WebApp[Web Application<br/>Servers]
        API --> DBProxy[Database Proxy]
        
        WebApp --> StaticAssets[Static Asset<br/>Storage]
        
        DBProxy --> PrimaryDB[(Primary Database<br/>Cluster)]
        DBProxy --> ReadReplicas[(Read Replicas)]
        
        Auth --> UserData[(User Data Store)]
    end
    
    subgraph "Git Storage Layer"
        WebApp --> GitService[Git Service]
        GitService --> ObjectStorage[(Git Objects<br/>Storage)]
        GitService --> RepoDB[(Repository<br/>Metadata DB)]
        
        ObjectStorage --- BackupService[Backup &<br/>Replication Service]
    end
    
    subgraph "Auxiliary Services"
        WebApp --> Search[Search Service]
        WebApp --> CI_CD[CI/CD Runners]
        WebApp --> Notification[Notification<br/>Service]
        
        Search --> SearchIndex[(Search Index)]
        CI_CD --> ArtifactStorage[(Build Artifacts<br/>Storage)]
        Notification --> MessageQueue[(Message Queue)]
    end
    
    subgraph "Regional Replication"
        BackupService --> GeoReplica1[(Geographic<br/>Replica 1)]
        BackupService --> GeoReplica2[(Geographic<br/>Replica 2)]
        BackupService --> GeoReplica3[(Geographic<br/>Replica 3)]
    end
    
    Admin[Admin Users] --> FW
    Developers[Developers] --> FW
    CITools[External CI/CD<br/>Tools] --> FW

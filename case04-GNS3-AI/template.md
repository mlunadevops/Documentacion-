# Technical Documentation: Automated VM Restoration from Proxmox Backup Server (PBS)

## Traffic Manipulation via the Weight Attribute
**CCNP Miguelangel Luna**

---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |
| **02** | [Packet Tracert & VS CODE](./case-02-PT-MCP-VS-Code/) | Conecta Packet Tracert con MCP |
| **03** | [Generar un Archivo Word desde Markdown usando Phyton](./case-03-Markdown-Word-Using-Phyton/) | Convierte un MD a Word usando Phyton |
| **04** | [GNS3 AI](./case04-GNS3-AI/) | Conexion GNS3 MCP. |

[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework

### Proxmox Backup Server (PBS):
Proxmox Backup Server is an open-source enterprise backup solution designed to back up and restore virtual machines (VMs), containers (CTs), and physical hosts. It utilizes **chunk-based deduplication, meaning only new or modified blocks of data are stored during each backup, drastically reducing disk space usage and optimizing network bandwidth.**

### Virtual Machine Recovery Process
Recovering (restoring) a VM involves rebuilding its virtual disks and configuration files from a snapshot stored on the PBS. The standard process in Proxmox VE (PVE) relies on native commands such as `qmrestore` and low-level tools (`pbs-restore`), which:
1. Query metadata and block indexes of the backup from the remote server.
2. Allocate the required virtual volumes in the local node storage (e.g., `local-lvm`).
3. Discover and concurrently download missing data chunks from the PBS repository to write them to the target disks.

### The `jq` Tool
`jq` is a lightweight and flexible command-line JSON processor. In the context of this script, it is completely indispensable because the Proxmox VE REST API responds exclusively in JSON format. `jq` allows you to filter, parse, and extract specific data—such as available PBS storage lists or snapshot identifiers—cleanly inside shell scripts.

**JQ Tool (RTA - AS 100):**

```text
apt update && apt install -y jq
```

---

## 2. Prerequisites
Before deploying and executing the script on any new Proxmox VE server, ensure the following requirements are met:
1. **Proxmox VE Connected to PBS:** The PVE node must have the Proxmox Backup Server storage added to its configuration.
2. **Dependency Installation (`jq`):** The JSON processor must be present on the base operating system.
3. **Proxmox API Token:** An authentication token with administrator privileges is required to interact with the local API without needing plain-text passwords.

## 3. Implementation and Deployment Steps
Follow these steps on any new Proxmox VE server to make the restoration script fully operational:

### Step 1: Install the `jq` Dependency
Run the following command in the terminal to install the JSON processor:





## 2. Topology and BGP Neighbor Establishment

The topology consists of four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

![BGP WEIGTH](images/01Topologia.jpg)

 four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

## 3. BGP Configuration:



### 4. BGP Configuration:

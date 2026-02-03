# Environment Setup

This section covers the base environment used to build the Wazuh SIEM lab.

## Host System
- OS: Windows
- Virtualization: Oracle VirtualBox

## Virtual Machines
### Wazuh Manager VM
- OS: Ubuntu Server 24.04
- Purpose: Wazuh Manager, Indexer, Dashboard

### Linux Agent VM
- OS: Ubuntu 22.04
- Purpose: Log and FIM data source

## Network Configuration
Two network adapters are used:

### Adapter 1 – NAT
- Provides internet access
- Used for package installation and updates

### Adapter 2 – Host-only
- Enables host-to-VM access
- Allows agent–manager communication

This dual-adapter design avoids connectivity issues
commonly seen with bridged networking.


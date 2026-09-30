# Domain Infrastructure Lab Configuration - NMG.com

This repository details the step-by-step implementation, provisioning, and policy deployment configurations executed to establish the core network infrastructure for the **NMG.com** corporate domain framework.

## 🛠️ Phase 1 & 2: Environment Provisioning & Network Bindings
*   **Virtual Machine Container**: Provisioned a 64-bit virtual sandbox container named **`NMG-DC01`** utilizing Oracle VirtualBox.
*   **Hardware Allocation**: 
    *   **RAM**: Allocated `4096 MB` (4GB) Base Memory.
    *   **Processors**: Allocated `2` vCPUs.
    *   **Storage**: Allocated a `40.00 GB` virtual hard disk.
*   **Network Isolation**: Adjusted the virtual adapter layout from default NAT to a **Bridged Adapter** to ensure discrete network visibility.
*   **Static IP Allocation**: Assigned static IPv4 parameters to isolate the server as an authoritative domain asset:
    *   **IP Address**: `192.168.10.10`
    *   **Subnet Mask**: `255.255.255.0`
    *   **Default Gateway**: `192.168.10.1`
    *   **Preferred DNS Server**: `192.168.10.10` *(Self-referencing loopback binding)*
*   **Identity Resolution**: Reconfigured the system hostname from default Windows template identifiers to the static designation **`NMG-DC01`**, followed by a scheduled system reboot.

## 🌲 Phase 3: Active Directory Domain Services (AD DS) Role
*   **Role Installation**: Deployed core system libraries using the *Add Roles and Features Wizard* inside the Server Manager Dashboard.
*   **Forest Promotion**: Promoted the virtual resource to an authoritative root domain controller, instantiating the standalone directory tree forest: **`NMG.com`**.
*   **Security Mechanisms**: Activated default Global Catalog features and configured Directory Services Restore Mode (DSRM) protective credentials.

## 👥 Phase 4: Directory Object Infrastructure
*   **Organizational Unit (OU)**: Created a structured logical directory boundary path named **`NMG_Objects`** to cleanly segregate domain assets.
*   **Security Groups**: Built two high-level global security groups inside the target OU path:
    *   `NMG_Admins` *(Administrative delegation controls)*
    *   `NMG_Staff` *(Standard structural object containment)*
*   **User Account Provisioning**: Provisioned an individual administrative user profile within the container path:
    *   **Display Identity**: `Cecil Sparks II`
    *   **User Logon Name**: `csparks@NMG.com`
    *   **Security Policies**: Explicitly adjusted attributes to `Password Never Expires` and added the account to the **`Domain Admins`** and **`NMG_Admins`** security context directories.

## 🔒 Phase 5: Enterprise Group Policy Deployment
*   **GPO Generation**: Created and linked a custom policy object named **`NMG_Global_Restrictions`** to the root level of the `NMG.com` hierarchy tree.
*   **Control Panel Lockdown**: Enabled systemic structural controls within the registry policy block:
    *   **Path**: `User Configuration` ➔ `Policies` ➔ `Administrative Templates` ➔ `Control Panel`
    *   **Rule Enforcement**: Activated **`Prohibit access to Control Panel and PC settings`** to restrict standard administrative settings modification panels.
*   **Forced Sync Validation**: Evaluated and validated the security changes immediately across all endpoint paths using the elevated command execution layer:
    ```bash
    gpupdate /force
    ```

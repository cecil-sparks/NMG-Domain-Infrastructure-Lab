# Domain Infrastructure Lab Configuration - NMG.com

This repository details the step-by-step implementation, provisioning, and policy deployment configurations executed to establish the core network infrastructure for the **NMG.com** corporate domain framework.

## 🛠️ Phase 1 & 2: Environment Provisioning & Network Bindings (Day 1)
*   **Virtual Machine Container**: Provisioned a 64-bit virtual sandbox container named **`NMG-DC01-New`** utilizing Oracle VirtualBox.
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
*   **Identity Resolution**: Reconfigured the system hostname from default Windows template identifiers to the static designation **`NMG-DC01-New`**, followed by a scheduled system reboot.

## 🌲 Phase 3: Active Directory Domain Services (AD DS) Role (Day 1)
*   **Role Installation**: Deployed core system libraries using the *Add Roles and Features Wizard* inside the Server Manager Dashboard.
*   **Forest Promotion**: Promoted the virtual resource to an authoritative root domain controller, instantiating the standalone directory tree forest: **`NMG.com`**.
*   **Health Validation**: Executed systemic domain controller diagnostics via elevated command line interface, achieving passing markers across all critical testing sectors:
    ```bash
    dcdiag
    ```

## 👥 Phase 4: Directory Object Infrastructure (Day 1)
*   **Organizational Unit (OU)**: Created a structured logical directory boundary path named **`NMG_Objects`** to cleanly segregate domain assets.
*   **Security Groups**: Built two high-level global security groups inside the target OU path:
    *   `NMG_Admins` *(Administrative delegation controls)*
    *   `NMG_Staff` *(Standard structural object containment)*
*   **User Account Provisioning**: Provisioned an individual administrative user profile within the container path:
    *   **Display Identity**: `Cecil Sparks II`
    *   **User Logon Name**: `csparks@NMG.com`
    *   **Security Policies**: Explicitly adjusted attributes to `Password Never Expires` and added the account to the **`Domain Admins`** and **`NMG_Admins`** security context directories.

## 🔒 Phase 5: Enterprise Group Policy Deployment (Day 1)
*   **GPO Generation**: Created and linked a custom policy object named **`NMG_Global_Restrictions`** to the root level of the `NMG.com` hierarchy tree.
*   **Control Panel Lockdown**: Enabled systemic structural controls within the registry policy block:
    *   **Path**: `User Configuration` ➔ `Policies` ➔ `Administrative Templates` ➔ `Control Panel`
    *   **Rule Enforcement**: Activated **`Prohibit access to Control Panel and PC settings`** to restrict standard administrative settings modification panels.
*   **Forced Sync Validation**: Evaluated and validated the security changes immediately across all endpoint paths using the elevated command execution layer:
    ```bash
    gpupdate /force
    ```

---

## 📂 Day 2 Challenge: Organizing Chaos
Established a scalable, standardized structural hierarchy within the `NMG.com` directory tree to eliminate ad-hoc user account creation and optimize data control boundaries.

### 🏢 Phase 1: Departmental Organizational Units (OUs)
Created four distinct, dedicated department containment folders directly beneath the root domain tree:
*   **`Finance`**: Structural container for financial roles and accounting policies.
*   **`HR`**: Structural container for human resources data and personnel management.
*   **`IT`**: Structural container for system administrators and technical infrastructure assets.
*   **`Operations`**: Structural container for scheduling, workflow identities, and production tracking.

### 🔐 Phase 2: Role-Based Security Groups
Provisioned global security group objects inside each unique department folder to establish centralized, role-based access management:
*   `Finance\Finance-Users`
*   `HR\HR-Users`
*   `IT\IT-Users`
*   `Operations\Operations-Users`

### 🎯 Phase 3: Architectural Intent & Scalability Goals
*   **Granular Policy Enforcement**: Segregating departments into isolated OUs permits granular assignment of department-specific security boundaries (e.g., forcing shorter password rotation requirements on financial profiles).
*   **Centralized Access Mapping**: Managing resource permissions (such as shared storage volumes or restricted cloud tooling) is executed entirely through group memberships rather than manual per-user configurations, maintaining a strict Zero Trust access posture.

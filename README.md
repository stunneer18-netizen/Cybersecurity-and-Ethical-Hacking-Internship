# 🔐 Cybersecurity Testing Lab Environment Setup

**Building an isolated multi-node virtual laboratory for penetration testing, traffic analysis, and network security practice.**

---

## 📌 Project Overview

This repository documents the structural installation, configuration, and verification of a professional **Cybersecurity and Network Security Laboratory** built inside a Type-2 hypervisor. 

The purpose of this project is to establish a containerized sandbox environment where offensive security utilities, automated network reconnaissance, vulnerability assessments, and traffic monitoring strategies can be simulated safely without introducing risks to the physical host network or surrounding infrastructure.

The environment utilizes a private, custom **NAT Network** architecture, ensuring that all deployed attacker platforms and target virtual systems communicate with high reliability while retaining controlled outbound internet connectivity for system updates.

---

## 🎯 Objectives

- **Hypervisor Implementation:** Install and configure Oracle VirtualBox to handle cross-platform virtualization layers.
- **Offensive Workspace Deployment:** Import and optimize a dedicated Kali Linux penetration testing virtual machine.
- **Victim Infrastructure Integration:** Deploy diverse target instances, including a Windows 10 workstation clone, an Android 9.0 mobile emulator environment, and an intentionally unpatched Metasploitable 2 Linux node.
- **Private Subnet Bridging:** Establish a private virtual switch utilizing a `10.0.0.0/24` network framework with active DHCP services.
- **Static Address Allocation:** Manually align and assign consistent IPv4 configurations across all nodes to facilitate clear documentation and stable connection parameters.
- **Connectivity & DNS Verification:** Perform rigorous inter-VM ICMP packet sweeps and name resolution queries to validate network stability.
- **Baseline Snapshotting:** Capture verified recovery points for all virtual assets to secure a clean rolling baseline for future exercises.

---

## 🏗️ Lab Architecture

The environment architecture separates the physical host machine from the virtual sandbox using the following topology:

![Custom Lab Architecture](assets/1.%20Lab%20layout.png)

---

## ⚙️ System Configuration Matrix

| Component | Detail / Configuration Parameters |
| :--- | :--- |
| **🖥️ Host Operating System** | Windows 10 Pro (Physical Machine) |
| **🧰 Hypervisor Platform** | Oracle VirtualBox Manager |
| **🌐 Virtual Network Mode** | Custom NAT Network (**NatNetwork**) |
| **📡 Subnet Network Address** | `10.0.0.0/24` |
| **🚪 Virtual Default Gateway** | `10.0.0.1` |
| **🌍 Upstream DNS Server** | `8.8.8.8` |
| **🐉 Attacker Machine (Kali)** | Deployed Address: **`10.0.0.2`** (RAM: 2048 MB) |
| **📱 Mobile Target Node** | Deployed Address: **`10.0.0.9`** (Android 9.0 R2) |
| **🪟 Desktop Target Node** | Deployed Address: **`10.0.0.10`** (Windows 10 Workstation Clone) |
| **🐧 Linux Target Node** | Deployed Address: **`10.0.0.16`** (Metasploitable 2 Frame) |
| **🔮 Available Lab Range** | `10.0.0.3` to `10.0.0.99` (Reserved for future target VMs) |

---

## 🪜 Lab Setup Procedure

### Step 1: Archive Processing and Environment Prep
- Installed the open-source file archiver tool **7-Zip** on the host machine to handle compressed Open Virtualization Archive (`.ova`) files and `.7z` packages distributed during laboratory delivery.

### Step 2: Hypervisor Installation
- Compiled and initialized the primary Oracle VirtualBox virtualization engine package on the host platform.
- Enabled global environment preferences, ensuring bidirectional shared clipboard configurations and file drag-and-drop options were active.

### Step 3: Virtual NAT Network Configuration
- Navigated to `VirtualBox Preferences -> Network` and added a new private virtual switch named `NatNetwork`.
- Explicitly configured the network block interface parameters:
  - Network CIDR Subnet: `10.0.0.0/24`
  - DHCP Server Allocation: **Enabled** (Managing automatic range attachments)
  - IPv6 Support: **Disabled**

### Step 4: Virtual Machine Deployment & Resource Provisioning
- Downloaded pre-configured security assets and imported the Kali Linux, Windows Workstation, Android, and Metasploitable images as discrete hypervisor appliances.
- Sliced and mapped physical hardware metrics to ensure optimal VM stability:
  - Provided **2048 MB RAM** allocation to the main Kali terminal block.
  - Set the virtual network hardware interface controller options to link directly to **NAT Network**, selecting `NatNetwork` from the dropped property selector layout.

### Step 5: Network Adapter Alignment & Static Address Mapping
- Initialized each guest operating system engine and navigated to their respective interface settings to substitute standard dynamic flags for missing parameters:
  - **Kali Linux:** Configured `Wired connection 1` under Manual method matching IPv4 properties: IP `10.0.0.2`, Subnet Mask `24`, Gateway `10.0.0.1`, DNS `8.8.8.8`.
  - **Windows 10 Workstation:** Navigated to Network Connections Properties, manually modifying the Internet Protocol Version 4 (TCP/IPv4) mask values to IP `10.0.0.10` and Netmask `255.255.255.0`.
  - **Android 9.0 Node:** Updated the virtual Wi-Fi configuration properties panel, switching the IP parameters to Static mode at `10.0.0.9`.

### Step 6: Capturing Clean System Baselines
- Shut down all operating machine processes and utilized the VirtualBox snapshot utility to generate a clean, unadulterated baseline recovery track named `Snapshot 1`. This establishes a known-good restore point that protects our core lab states from software damage or configuration breakdowns during upcoming testing simulations.

---

## 🔎 Verification & Traffic Testing Analysis

A comprehensive diagnostic test matrix was executed from the attacker machine shell window to verify connection properties, check interface routing, and confirm that packet data flows seamlessly across the shared internal switch with zero anomalies.

As shown in the verification outputs, **all victim virtual machines are completely reachable** with a 100% success rate across the local communication channels.

### Diagnostic Verification Checklist

| Test Item | Command Matrix | Target Metric / Expected Result | State |
| :--- | :--- | :--- | :---: |
| **Verify Local IP** | `ip a` | Ensure interface maps cleanly to static string `10.0.0.2/24` | **PASS** |
| **Probe Gateway** | `ping -c 4 10.0.0.1` | Check communication latency to virtual default gateway node | **PASS** |
| **Mobile Node Link** | `ping -c 4 10.0.0.9` | Verify connection path stability to the Android target framework | **PASS** |
| **Workstation Link** | `ping -c 4 10.0.0.10`| Verify connection path stability to the Windows 10 workstation | **PASS** |
| **Outbound Check** | `ping -c 4 8.8.8.8` | Verify external translation engines route traffic to public space | **PASS** |
| **DNS Resolution** | `nslookup google.com`| Check recursive name parsing functionality on local DNS ports | **PASS** |

### Live Terminal Execution Trace Examples

#### 1. Verifying the Android Node Connection Path (`10.0.0.9`)
```bash
kali@kali:~\$ ping -c 4 10.0.0.9
PING 10.0.0.9 (10.0.0.9) 56(84) bytes of data.
64 bytes from 10.0.0.9: icmp_seq=1 ttl=64 time=0.472 ms
64 bytes from 10.0.0.9: icmp_seq=2 ttl=64 time=0.333 ms
64 bytes from 10.0.0.9: icmp_seq=3 ttl=64 time=0.275 ms
64 bytes from 10.0.0.9: icmp_seq=4 ttl=64 time=0.307 ms

--- 10.0.0.9 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3042ms
rtt min/avg/max/mdev = 0.275/0.346/0.472/0.076 ms
```

#### 2. Verifying the Windows 10 Workspace Connection Path (`10.0.0.10`)
```bash
kali@kali:~\$ ping -c 4 10.0.0.10
PING 10.0.0.10 (10.0.0.10) 56(84) bytes of data.
64 bytes from 10.0.0.10: icmp_seq=1 ttl=128 time=0.375 ms
64 bytes from 10.0.0.10: icmp_seq=2 ttl=128 time=0.297 ms
64 bytes from 10.0.0.10: icmp_seq=3 ttl=128 time=0.318 ms
64 bytes from 10.0.0.10: icmp_seq=4 ttl=128 time=0.308 ms

--- 10.0.0.10 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3014ms
rtt min/avg/max/mdev = 0.297/0.324/0.375/0.030 ms
```

---

## 🖼️ Hypervisor Verification Proofs

The configuration metrics and active network loops have been visually cataloged within the local assets folder:

### Deployed Subnet Mapping Preferences
![Subnet Preferences](assets/2.%20NATNetwork%20profile%20creation.png)
*Figure 1: VirtualBox Network tools pane confirming that the active network interface (NatNetwork) is assigned to the 10.0.0.0/24 network.*

### Attacker Network Configuration Details
![Kali Settings](assets/3.%20Kali%20Manual%20IP.png)
*Figure 2: Internal Kali Linux Network Connections editor panel, validating the manual adjustment of Wired connection 1 to an address string of 10.0.0.2.*

### Windows Node Local Protocol Settings
![Windows Network Settings](assets/4.%20Windows%20manual%20IP.png)
*Figure 3: Internal Windows 10 target panel tracking the active assignment of an IPv4 address to 10.0.0.10.*

### Android Static Address Alignment
![Android Settings](assets/5.%20Android%20manual%20IP.png)
*Figure 4: Target Android system interface details pane confirming successful configuration properties using manual static IP allocation parameters at 10.0.0.9.*

### Inter-VM Traffic Analysis Outputs
![Ping Verification](assets/6.%20Attacker%20to%20victim%20VMs%20ping.png)
*Figure 5: Terminal console pane outputting the active ping loop checks against the target nodes, proving that traffic flows seamlessly with 0% packet loss.*

---

## 🐞 Problems Encountered & Technical Resolutions

### Problem 1: External Internet Failure After Manual IP Configuration
**Symptom:** After applying static address metrics to the Kali Linux desktop profile, all outbound communication to the external internet broke, despite internal inter-VM ping tests operating normally.
**Resolution:** This is a common Duplicate Address Detection (DAD) delay issue affecting network interface initializations in virtual machine settings. The problem was mitigated by opening a root terminal shell and running the following `nmcli` connection parameter scripts to clear the DAD constraint and restart the interface thread:
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

### Problem 2: Hypervisor Failure Due to Disabled Virtualization Settings
**Symptom:** The deployed virtual appliances failed to initialize on their first boot, throwing a critical system hardware acceleration error flag (`VT-x/AMD-V is disabled`).
**Resolution:** This error occurs when hardware virtualization constraints remain locked inside the physical host machine’s motherboard firmware. To resolve this, the host system was restarted directly into its BIOS/UEFI utility setup screen. Under Advanced CPU Configurations, **Intel Virtualization Technology** (or **SVM Mode**) was toggled from disabled to **Enabled**. The configuration was saved and the machine rebooted, allowing the hypervisor to safely spawn the virtual testing instances.

---

## 💡 Practical Insights Acquired

Through this deployment project, several critical enterprise architectural concepts were mastered:

1. **NAT vs. NAT Network Topologies:** Differentiated standard NAT (which isolates individual machines inside distinct outbound containers) from a NAT Network structure (which links multiple virtual endpoints to a shared internal switch). A NAT Network allows for local network discovery and inter-VM scanning while seamlessly handling network address translations for outbound internet routing.
2. **Static Network Engineering:** Developed practical familiarity with manually assigning network settings (IP addresses, network masks, default gateways, and DNS addresses) within both Linux and Windows terminal shells.
3. **Forensic Recovery Management:** Recognized the strategic value of taking system snapshots *prior* to executing aggressive security tests or dangerous script files. This process secures a quick recovery vector to restore the virtual machines to a clean state if a lab payload accidentally corrupts system configurations.

---

## 🔐 Ethical Boundaries & Usage Agreement
⚠️ **Disclaimer:** This virtual laboratory environment has been configured exclusively for educational purposes, authorized security testing simulations, and private training modules. Running active network discovery sweeps, automated scanning tools, or penetration testing payloads against unauthorized external networks or third-party assets without clear, written consent is strictly illegal and violates global network management regulations.

---

## 🔗 Deployed Component Manifest

- **Virtualization Core Platform Engine:** [Oracle VirtualBox Manager Archive](https://virtualbox.org)
- **Offensive Security Operating Linux Suite:** [Kali Linux Virtual Appliance Mirror Distribution](https://kali.org)
- **File Compression Utility Infrastructure:** [7-Zip Resource Page](https://7-zip.org)

---

## 👤 Author Profile

**Siphiwe Toise**  
*Aspiring Network Security Professional*  
Networkwalks Academy Internship Task Workspace  

***

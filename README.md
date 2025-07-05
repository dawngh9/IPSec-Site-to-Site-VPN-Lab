## Overview

This project demonstrates an IPSec Site-to-Site VPN implementation using Cisco IOS routers within a GNS3 simulated network environment. It establishes a secure, encrypted tunnel between two distinct private networks over a simulated public internet connection.

## Key Components

* **Network Emulation:** GNS3 (with GNS3 VM)
* **VPN Endpoints:** Cisco IOS Routers (e.g., c7200)
* **VPN Protocol:** IPSec (IKEv1 Phase 1 & Phase 2)
* **Simulated WAN:** GNS3 Cloud nodes connected to `VMnet8 (NAT)`

## Lab Topology

```

[Site A - LAN: 192.168.1.0/24]                      [Site B - LAN: 192.168.2.0/24]

PC1 --- Switch A --- R1 --- (WAN/Internet) --- R2 --- Switch B --- PC2

```
*(Optional: Insert a screenshot of your GNS3 topology here: ![Lab Topology]([your-image-link-here]))*

## Key IP Addressing

* **R1 (Site A Router):**
    * LAN: `192.168.1.1/24`
    * WAN: DHCP (e.g., `192.168.188.139`)
* **PC1 (Site A Client):** `192.168.1.10/24` (Gateway: `192.168.1.1`)
* **R2 (Site B Router):**
    * LAN: `192.168.2.1/24`
    * WAN: DHCP (e.g., `192.168.188.140`)
* **PC2 (Site B Client):** `192.168.2.10/24` (Gateway: `192.168.2.1`)

## Quick Start / How to Run

1.  **Prerequisites:** Ensure GNS3 (with GNS3 VM and Cisco IOS images) is installed and operational.
2.  **Load Project:** Open the GNS3 project file (or recreate the topology as per the detailed guide).
3.  **Configure Clouds:** Verify `Cloud_A` and `Cloud_B` are linked to your `GNS3 VM`'s `VMnet8 (NAT)` interface.
4.  **Start Devices:** Power on all devices in the GNS3 workspace.
5.  **Apply Configurations:** Apply the provided Cisco IOS and VPCS configurations (refer to a `detailed_config.md` or similar file if available, or the full guide).
6.  **Verify WAN Connectivity:** Ensure `R1` can `ping` `R2`'s WAN IP, and vice-versa.
7.  **Initiate VPN:** From `PC1` console, `ping 192.168.2.10` to trigger the VPN tunnel establishment.

## Verification

After initiating traffic:

* **Router Console (`R1` or `R2`):**
    * Check ISAKMP SA: `show crypto isakmp sa` (Look for `QM_IDLE` state).
    * Check IPSec SA: `show crypto ipsec sa` (Look for increasing `encaps`/`decaps` counters and `Status: ACTIVE`).
* **PC Console (`PC1`):**
    * Verify ping: `ping 192.168.2.10` (Should now be successful).

## Troubleshooting

If the VPN fails to establish, common issues include:
* Mismatch in ISAKMP/IPSec policy parameters (encryption, hash, group, lifetime, transform-set).
* Incorrect pre-shared key.
* Incorrectly defined "interesting traffic" ACLs.
* No underlying WAN connectivity between the routers.

## Contact

For questions or support, please open an issue on this GitHub repository.

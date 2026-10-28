VirtualBox Lab Setup — Cybersecurity Practice
Author: Ritesh Kumawat
Project: Week 1 — Project Module 1: Lab Setup with VirtualBox and Kali Linux
Overview
This project documents the setup of a small virtual cybersecurity lab using Oracle VirtualBox and Kali Linux. The lab is intended for learning networking, Linux administration, and ethical-hacking fundamentals in an isolated environment.
Objectives
- Create a VirtualBox NAT Network using the 10.0.0.0/24 IPv4 subnet.
- Import Kali Linux as a virtual machine (VM).
- Connect the Kali VM to the custom NAT Network.
- Verify that Kali can reach the internet.
- Configure the required Kali address and VirtualBox sharing features, then save a VM snapshot.
Lab Environment
Component	Configuration
Virtualization software	Oracle VirtualBox
Guest operating system	Kali Linux (VirtualBox image)
NAT Network name	NatNetwork
IPv4 network prefix	10.0.0.0/24
VirtualBox DHCP server	Enabled in the captured settings
Required Kali IPv4 address	10.0.0.2/24 — verify in Kali before marking complete
Expected gateway from the lab guide	10.0.0.1
Connectivity test shown	ping 8.8.8.8 — successful replies, 0% packet loss in the screenshot


Note: The screenshots confirm the NAT Network, the imported Kali VM, and successful IP-level internet connectivity. They do not yet show Kali's assigned IPv4 address, shared-folder configuration, bidirectional clipboard/drag-and-drop settings, or the final snapshot. Verify and capture those items before presenting the whole task as fully complete.

Setup Steps
1. Install VirtualBox and obtain Kali Linux
1. Install VirtualBox for the host operating system.
2. Download the pre-built VirtualBox image from the official Kali Linux download page.
3. Extract the archive if required, then add/import the Kali VM into VirtualBox.
Official downloads:
- VirtualBox
- Kali Linux
2. Create the NAT Network
1. Open VirtualBox's global Network settings and select NAT Networks.
2. Create or select NatNetwork.
3. Set IPv4 Prefix to 10.0.0.0/24.
4. Keep Enable DHCP enabled as shown in the captured configuration.
5. Save the settings.
<img width="2050" height="1128" alt="Screenshot_20261027_213708" src="https://github.com/user-attachments/assets/4539bac5-9c1d-4810-9cb8-7514603c02e3" />

Figure 1. NAT Network configured with IPv4 prefix 10.0.0.0/24 and DHCP enabled.
3. Attach Kali to the NAT Network
1. Shut down the Kali VM before changing its hardware settings.
2. Open Kali VM → Settings → Network → Adapter 1.
3. Enable the network adapter and select NAT Network as the attachment type.
4. Choose NatNetwork and ensure Cable Connected is selected.
5. Save the settings.

Figure 2. Kali Linux VM imported in VirtualBox; the details panel shows Adapter 1 attached to the NatNetwork NAT Network.
4. Set Kali's IPv4 configuration
The assignment requires the Kali VM to use 10.0.0.2/24. In Kali's network connection settings, configure IPv4 manually using the values below if they are appropriate for your lab:
Field	Required value
IPv4 address	10.0.0.2
Prefix length	24
Gateway	10.0.0.1
DNS server	8.8.8.8


Make sure no other VM is using 10.0.0.2. As DHCP is enabled on the NAT Network, avoid address conflicts when assigning the required static address.

Verify the interface and route from Kali Terminal:
ip -br addr
ip route
The active Kali network interface should show 10.0.0.2/24, and the default route should use the configured gateway.
5. Test network and internet connectivity
Run the following tests in Kali Terminal:
ping -c 4 10.0.0.1
ping -c 4 8.8.8.8
ping -c 4 google.com
A successful ping 8.8.8.8 verifies IP-level reachability to that destination. A successful ping google.com also tests name resolution, provided ICMP traffic is permitted.

Figure 3. Kali Terminal showing successful replies from 8.8.8.8 and 0% packet loss in the captured test.
6. Enable clipboard, drag-and-drop, and shared folder
With the VM shut down, open its VirtualBox settings:
- Under General → Advanced, set Shared Clipboard to Bidirectional.
- Set Drag'n'Drop to Bidirectional.
- Under Shared Folders, add the host computer's Downloads folder.
- Set the shared-folder name to downloads, enable Auto-mount, and select Make Permanent. Grant full access only if appropriate for your host and lab needs.
The screenshots currently included in this repository do not show these settings, so add your own screenshot after configuring them.
7. Take a snapshot
After the IP address, internet access, and sharing settings are confirmed:
1. Open VirtualBox Manager and select the Kali VM.
2. Open Snapshots and choose Take.
3. Use a clear name such as Week1-Lab-Setup-Complete.
4. Save the snapshot.
Add a screenshot of the snapshot list before submission.
Evidence Screenshots
Evidence	Screenshot	Status based on current evidence
NAT Network subnet and DHCP	screenshots/nat-network-settings.png	Captured
Kali VM imported and attached to NAT Network	screenshots/kali-vm-overview.png	Captured
Internet ping to 8.8.8.8	screenshots/internet-connectivity-test.jpeg	Captured
Kali static IP 10.0.0.2/24	Add screenshot showing ip -br addr	Still to verify
Clipboard and drag-and-drop	Add VirtualBox General → Advanced screenshot	Still to verify
Host Downloads shared folder	Add VirtualBox Shared Folders screenshot	Still to verify
Final snapshot	Add VirtualBox Snapshots screenshot	Still to verify


Completion Checklist
- [x] NAT Network created with IPv4 prefix 10.0.0.0/24.
- [x] Kali Linux VM imported into VirtualBox.
- [x] Kali VM attached to NatNetwork.
- [x] Internet IP connectivity test captured.
- [ ] Verify Kali's actual IP is 10.0.0.2/24.
- [ ] Enable and verify bidirectional clipboard and drag-and-drop.
- [ ] Share the host Downloads folder.
- [ ] Take and capture the final VM snapshot.
Troubleshooting
Kali has no internet:
1. Confirm Adapter 1 is enabled and attached to NatNetwork.
2. Confirm the NAT Network prefix is 10.0.0.0/24.
3. Check the current IP address and route with ip -br addr and ip route.
4. Check that no other VM is using 10.0.0.2.
5. Test the gateway, public IP, and DNS separately using the ping commands above.
For issues specific to the VirtualBox/Kali versions used in the lab, consult the instructor's provided guide before applying version-specific commands.
Safety and Scope
Use this virtual lab for authorized learning and testing only. Test against systems you own or have explicit permission to assess. Keep vulnerable practice machines on an isolated lab network.
References
- Oracle VirtualBox Downloads
- Kali Linux — Get Kali
- Internship handout: WK1-PM1 — Week 1: Project Module 1 — Lab Setup VirtualBox and Kali Linux

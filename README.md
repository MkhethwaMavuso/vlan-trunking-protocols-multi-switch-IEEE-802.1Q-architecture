# vlan-trunking-protocols-multi-switch-IEEE-802.1Q-architecture
Multi-Switch Layer 2 Enterprise Access Topology featuring three interconnected Cisco 2960 Catalyst switches (Switch0, Switch1, and Switch2) joined via IEEE 802.1Q inter-switch trunk links to extend logical VLAN boundaries across physical switches.

🌐 Quick Overview & Network Specs
🟢 Architecture & Topology: Multi-Switch Layer 2 Enterprise Access Topology featuring three interconnected Cisco 2960 Catalyst switches (Switch0, Switch1, and Switch2) joined via IEEE 802.1Q inter-switch trunk links to extend logical VLAN boundaries across physical switches.

🔵 Departmental VLAN & IP Subnet Allocations:

VLAN 10 (HR Department):

PC0 connected to Switch0 (192.168.10.2/24)

Server0 connected to Switch2 (192.168.10.3/24)

VLAN 20 (Admin Department):

PC2 connected to Switch0 (192.168.20.2/24)

PC1 connected to Switch1 (192.168.20.3/24)

VLAN 30 (IT Department):

PC3 connected to Switch2 (192.168.30.2/24)

🟣 Layer 2 Inter-Switch Trunk Infrastructure:

Switch0 ↔ Switch1 and Switch1 ↔ Switch2 links are explicitly configured as IEEE 802.1Q trunks, allowing frame tagging and multiplexing of multiple VLANs over shared physical links.

💡 Key Technical Insights & What This Lab Demonstrates
🔍 IEEE 802.1Q Frame Tagging: Demonstrates how 802.1Q inserts a 4-byte VLAN tag (TPID 0x8100 + 12-bit VLAN ID) into Ethernet frames traveling over trunk links to preserve VLAN identification across switch boundaries.

⚡ Broadcast Domain Isolation & Trunk Transport: Proves that workstations in the same VLAN (e.g., PC0 and Server0 in VLAN 10, or PC2 and PC1 in VLAN 20) can communicate seamlessly across intermediate switches, while traffic between different VLANs remains isolated at Layer 2.

🛠️ Native VLAN & Security Best Practices: Emphasizes native VLAN alignment across trunk endpoints to ensure untagged control traffic (e.g., CDP, DTP, STP) is properly processed and prevent VLAN hopping vulnerabilities.

🛡️ Access Port vs. Trunk Port Differentiation: Illustrates access port configuration (untagged, assigned to a single VLAN) versus trunk port configuration (tagged, carrying multiple VLANs).

🛠️ Essential Cisco CLI Configuration Snippets
Configuring Inter-Switch Trunk Links (Switch1)
Cisco CLI
interface FastEthernet0/23
 description Trunk Link to Switch0
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
!
interface FastEthernet0/24
 description Trunk Link to Switch2
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
Configuring Departmental Access Ports (Switch0)
Cisco CLI
vlan 10
 name HR
vlan 20
 name Admin
!
interface FastEthernet0/1
 description Access Port for PC0 (HR)
 switchport mode access
 switchport access vlan 10
!
interface FastEthernet0/2
 description Access Port for PC2 (Admin)
 switchport mode access
 switchport access vlan 20
🧪 Verification & Audit Commands
Bash
# Verify active VLAN definitions, assigned ports, and status
show vlan brief

# Inspect active IEEE 802.1Q trunk links, operational modes, and allowed VLANs
show interfaces trunk

# Verify MAC address table entries mapped to specific VLAN IDs
show mac address-table

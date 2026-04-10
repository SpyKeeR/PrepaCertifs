![](media/image1.jpg)

> Chapter 15: IP Services
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 15 Content
>
> **This chapter covers the following content:**
>
> **Time Synchronization -** This section describes the need for
> synchronizing time in an environment and covers Network Time Protocol
> and its operations to keep time consistent across devices.
>
> **First-Hop Redundancy Protocol -** This section gives details on how
> multiple routers can provide resilient gateway functionality to hosts
> at the Layer 2/Layer 3 boundaries.
>
> **Network Address Translation (NAT) -** This section explains how a
> router can translate IP addresses from one network realm to another.
>
> Time Synchronization
>
> • A device's system time is used to measure periods of idle state or
> computation. It is important that time is consistent on a system
> because applications often use the system time to tune internal
> processes.
>
> • The rate a device can maintain its time can deviate from device to
> device. Time intervals can vary from one device to another and the
> times would eventually begin to drift away from each other.
>
> Time Synchronization
>
> It is important that a device's system time is consistent, and from
> the perspective of managing a
>
> network, that the time be synchronized between network devices for the
> several reasons:
>
> • Managing passwords that change at specific time intervals
>
> • Encryption key exchanges
>
> • Checking validity of certificates based on expiration date and time
>
> • Correlation of security-based events across multiple devices
> (routers, switches, firewalls, network access control systems, and so
> on)
>
> • Troubleshooting network devices and correlating events to identify
> the root cause of an event
>
> Network Time Protocol and Stratums
>
> • Network Time Protocol (NTP) is used to synchronize a set of network
> clocks in a distributed client/server architecture.
>
> • NTP is a UDP-based protocol that connects with servers on port 123.
> The client source port
>
> is dynamic.
>
> • NTP is based on a hierarchical concept of communication. At the top
> of the hierarchy are authoritative devices that operate as an NTP
> server with an atomic clock. The NTP client queries the NTP server for
> its time and then updates its time based on the response.
>
> • The NTP synchronization process is not fast, gaining an accuracy of
> tens of milliseconds requires hours or days of comparisons.
>
> • Stratums are used to identify the accuracy of the time clock source.
> NTP servers directly attached to an authoritative time source are
> stratum 1 servers.
>
> • An NTP client that queries a stratum 1 server is considered a
> stratum 2 client.
>
> • The higher the stratum, the greater the chance of deviation in time
> from the authoritative time source due to the number of time drifts
> between the NTP stratums.
>
> NTP Configuration
>
> ![](media/image2.jpg)To configure an NTP client use the global command
> **ntp** *ip-address* \[**prefer**\] \[**source** *interface-id*\]. The
> keywork **prefer** indicates which NTP server to use for time
> synchronization. The command **ntp master** *stratum-number* to
> statically set the stratum for a device when it acts as an NTP server.
>
> NTP Status and Associations
>
> The command **show ntp status** displays the status of the NTP
> service. It shows the following:
>
> • Whether the hardware clock is synchronized to the software clock,
> the stratum reference of the local device, and the reference clock
> identifier (local or IP address)
>
> • The frequency and precision of the clock
>
> • The NTP uptime and granularity
>
> • The reference time
>
> • The clock offset and delay between the client and the lower-level
> stratum server
>
> • Root dispersion and peer dispersion
>
> • NTP loopfilter
>
> • Polling interval and time since last update

![](media/image3.jpg)

> A streamlined version of the NTP server status and delay can be viewed
> using the command **show ntp associations**.
>
> Stratum Preference
>
> An NTP client configured with multiple NTP servers will only use the
> NTP server with the lowest stratum.
>
> ![](media/image4.jpg)If R2 crashes, preventing R4 from reaching R1, R4
> will synchronize with R3 and become a stratum 4 time device. When R2
> recovers, R4 will synchronize with R1 and become a stratum 2 device
> again.

![](media/image5.jpg)

> An NTP client will change it's time to that of the NTP server.
> However, an NTP server does not change its time to reflect an NTP
> client. NTP peers act as clients and servers to each other. They can
> query and synchronize their time to each other. NTP peers are
> configured with the command **ntp peer** *ip-address*.
>
> First-Hop Redundancy
>
> Protocol
>
> • Network resiliency is a key component of network design.
>
> • Network resiliency can be accomplished by adding redundant devices
> such as Layer 2 switches or Layer 3 routers into a topology.
>
> ![](media/image7.jpg)Network Resiliency/First Hop Redundancy Protocols
>
> The figure shows the concept of adding resiliency
>
> to the network. In both scenarios:
>
> • Two devices (172.16.1.2 and 172.16.1.3) can
>
> be the PC's gateway.
>
> • There are two resilient Layer 2 links that connect SW6 to a switch
> that can connect the PC to either gateway.
>
> First-hop redundancy protocols (FHRPs) solve the problem of end
> devices configuring multiple gateways. They do this by creating a
> virtual IP (VIP) gateway that is shared between the Layer 3 devices.
> The following are FHRPs:
>
> • Hot Standby Router Protocol (HSRP)
>
> • Virtual Router Redundancy Protocol (VRRP)
>
> • Gateway Load Balancing Protocol (GLBP)
>
> Object Tracking
>
> ![](media/image8.jpg)Object tracking offers a flexible and
> customizable mechanism for linking with FHRPs and other routing
> components.
>
> ![](media/image9.jpg)Users can track specific objects in the network
> and take necessary action when any object's state change affects the
> network traffic.
>
> To track routes in the routing table use the command **track**
> *object-number* **ip route** *route/prefix-length* **reachability**.
> The status of object tracking can be viewed with the command **show
> track** \[*object-number*\].
>
> ![](media/image10.jpg)To track an interface's line protocol state use
> the command **track** *object-number* **interface** *interface-id*
> **line-protocol**.
>
> The example shows R2 being configured
>
> for tracking the Gi0/1 interface toward
>
> R3.
>
> ![](media/image11.jpg)Shutting down R2's Gi0/1 interface changed the
> tracked object state on R1 and R2 to a down state.
>
> Object tracking works with protocols such as Hot Standby Router
> Protocol (HSRP), Virtual Router Redundancy Protocol (VRRP), and
> Gateway Load Balancing Protocol (GLBP). They take action when the
> state of an object changes.
>
> Hot Standby Router Protocol
>
> Hot Standby Routing Protocol (HSRP) is a Cisco proprietary protocol.
> It provides routing redundancy for hosts configured with a default
> gateway IP address.
>
> • A minimum of two devices are required to enable HSRP:
>
> • One device acts as the active device and takes care of forwarding
> the packets.
>
> • The other acts as a standby that is ready to take over the role of
> active device in the event of a failure.
>
> • A virtual IP address is configured on each HSRP-enabled interface
> that belongs to the
>
> same HSRP group. A virtual MAC address is also assigned for the group.
>
> • The active router receives and routes the packets destined for the
> virtual MAC address of the group.
>
> • HSRP-enabled interfaces send and receive multicast UDP-based hello
> messages to
>
> detect any failure and designate active and standby routers.
>
> • When the HSRP active router fails, the HSRP standby router assumes
> control of the virtual IP address and virtual MAC address of the
> group.
>
> HSRP Elections & Versions
>
> • A HSRP election selects the router with the highest priority
> (default is 100).
>
> • In the event of a tie in priority, the router with the highest IP
> address for the network segment is preferred.
>
> • HSRP does not support preemption by default. If a router with a
> lower priority becomes active, it stays active regardless if the
> superior router comes back online.
>
> • The transition of the HSRP active to the standby is transparent to
> all hosts on the segment because the MAC address moves with the
> virtual IP address.
>
> • HSRP has two versions, HSRPv1 and HSRPv2.
>
> ![](media/image12.jpg)
>
> Configuring HSRP Virtual IP Address
>
> The following steps show how to configure an HSRP virtual IP (VIP)
> gateway instance:
>
> **Step 1**. Define the HSRP instance by using the command **standby**
> *instance-id* **ip** *vip- address*.
>
> **Step 2**. (Optional) Configure HSRP router preemption with the
> command **standby** *instance- id* **preempt**.
>
> **Step 3.** (Optional) Configure the HSRP priority by using the
> command **standby** *instance-id*
>
> **priority** *priority*. The priority is a value between 0 and 255.
>
> **Step 4.** (Optional) Configure the HSRP MAC address with the command
> **standby** *instance- id* **mac-address** *mac-address*.
>
> **Step 5.** (Optional) Define the HSRP timers by using the command
> **standby** *instance-id* **timers** {*seconds* \| **msec**
> *milliseconds*}. HSRP can poll in intervals of 1 to 254 seconds or 15
> to 999 milliseconds
>
> **Step 6.** (Optional) Establish HSRP authentication by using the
> command **standby** *instance- id* **authentication** {*text-password*
> \| **text** *text-password* \| **md5** {**key-chain** *key-chain* \|
> **key- string** *key-string*}}.
>
> HSRP Configuration and State
>
> ![](media/image13.jpg)Example 15-9 shows a basic HSRP configuration
> for VLAN 10 on SW1 and SW2, using the HSRP instance 10 and the VIP
> gateway instance 172.16.10.1.
>
> ![](media/image14.jpg)Example 15 -10 shows the summarized HSRP status
> using the command **show standby** \[*interface-id*\] \[**brief**\].
>
> The **show standby** command gives more details into the HSRP state.
> It includes the number of state changes, time since last state change,
> VIP addresses, timers, preemption, priority and group name.
>
> ![](media/image15.jpg)HSRP provides the capability to link object
> tracking to priority.
>
> ![](media/image16.png)Example 15-12 shows the configuration of SW2
> where a tracked object is created against VLAN 1's interface line
> protocol, increasing the HSRP priority to 110, and linking HSRP to the
> tracked object so that the priority decrements by 20 if interface VLAN
> 1 goes down.
>
> Example 15-13 shows that the HSRP group on VLAN 10 on SW2 correlates
> the status of the tracked object for the VLAN 1 interface.

![](media/image17.jpg)

> Example 15-14 verifies the anticipated behavior by shutting down the
> VLAN 1 interface on SW2. The syslog messages indicate that the object
> track state changed immediately after the interface was shut down, and
> shortly thereafter, the HSRP role changed to a standby state.
>
> Virtual Router Redundancy Protocol
>
> Virtual Router Redundancy Protocol (VRRP) is an industry standard
> protocol that operates similarly to HSRP. However, the differences are
> as follows:
>
> • The preferred active router controlling the VIP gateway is called
> the master router. All
>
> other VRRP routers are known as backup routers.
>
> • VRRP enables preemption by default.
>
> • The MAC address of the VIP gateway uses the structure
> 0000.5e00.01xx, where xx reflects the group ID in hex.
>
> • VRRP uses the multicast address 224.0.0.18 for communication.
>
> There are currently two versions of VRRP:
>
> • VRRPv2: Supports IPv4
>
> • VRRPv3: Supports IPv4 and IPv6
>
> Legacy VRRP Configuration
>
> ![](media/image18.png)Early VRRP configurations supported only VRRPv2
> and was non-hierarchical in its configuration. The following are steps
> used to configure older software versions with VRRP:
>
> **Step 1.** Define the VRRP instance by using the
>
> command **vrrp** *instance-id* **ip** *vip-address*.
>
> **Step 2.** (Optional) Define the VRRP priority by using the command
> **vrrp** *instance-id* **priority** *priority*. The priority is a
> value between 0 and 255.
>
> **Step 3.** (Optional) Enable object tracking so that the priority is
> decremented when the object is false by using the command **vrrp**
> *instance-id* **track** *object-id* **decrement** *decrement-value*.
>
> **Step 4.** (Optional) Establish VRRP authentication by using the
> command vrrp instance-id authentication {*text- password* \| **text**
> *text-password* \| **md5** {**key-chain** *key- chain* \|
> **key-string** *key-string*}}
>
> ![](media/image19.png)VRRP State
>
> The command **show vrrp** \[**brief**\] provides an update on the VRRP
> group, along with other relevant information for troubleshooting.
> Example 15-16 shows the brief iteration of the command and 15-17 shows
> the detailed state of VRRP.
>
> Hierarchical VRRP Configuration
>
> The newer version of IOS XE software provides configuration of VRRP in
> a multi-address format that
>
> is hierarchical. The following are steps to configure hierarchical
> VRRP:
>
> ![](media/image21.jpg)**Step 1.** Enable VRRPv3 on the router by using
> the command **fhrp version vrrp v3**.
>
> **Step 2.** Define the VRRP instance by using the command
>
> **vrrp** *instance-id* **address-family** {**ipv4** \| **ipv6**}.
>
> **Step 3.** (Optional) Change VRRP to Version 2 by using the command
> **vrrpv2**. VRRPv2 and VRRPv3 are not compatible.
>
> **Step 4.** Define the gateway VIP by using the command
>
> **address** *ip-address*.
>
> **Step 5.** (Optional) Define the VRRP priority by using the command
> **priority** *priority*.
>
> **Step 6**. (Optional) Enable object tracking so that the priority is
> decremented when the object is false using the command **track**
> *object-id* **decrement** *decrement-value*.
>
> The status of the VRRP routers can be viewed with the command **show
> vrrp** \[**brief**\]. The output is identical to that
>
> of the legacy VRRP configuration.
>
> Global Load Balancing Protocol
>
> Global Load Balancing Protocol (GLBP) provides gateway redundancy and
> load-balancing capability to a network segment. It does this with an
> active/standby gateway and ensures that each member of the GLBP group
> forwards traffic to the appropriate gateway.
>
> The GLBP has two roles:
>
> • **Active virtual gateway (AVG):** The participating routers elect
> one AVG per GLBP group to respond to initial ARP requests for the VIP.
>
> • **Active virtual forwarder (AVF):** The AVF routes traffic received
> from assigned hosts. A unique virtual MAC address is created and
> assigned by the AVG to the AVFs. The AVF is assigned to a host when
> the AVG replies to the ARP request with the assigned AVF's virtual MAC
> address. The AVFs are also recognized as Fwd instances on the routers.
>
> GLBP supports four active AVFs and one AVG per GLBP group. A router
> can be an AVG and an AVF at the same time. In the event of a failure
> of the AVG, the AVG role is transferred to a standby AVG device. In
> the event of a failure of an AVF, another router takes over the
> forwarding responsibilities for that AVF, which includes the virtual
> MAC address for that instance.
>
> GLBP Configuration
>
> The following steps detail how to configure a GLBP:
>
> **Step 1.** Define the GLBP instance by using the
>
> ![](media/image22.jpg)command **glbp** *instance-id* **ip**
> *vip-address*.
>
> **Step 2.** (Optional) Configure GLBP preemption with the command
> **glbp** *instance-id* **preempt**.
>
> **Step 3**. (Optional) Define the GLBP priority by using the command
> **glbp** *instance-id* **priority** *priority*. The priority is a
> value between 0 and 255.
>
> **Step 4.** (Optional) Define the GLBP timers by using the command
> **glbp** *instance-id* **timers** {*hello-seconds*
>
> \| **msec** *hello-milliseconds*} {*hold-seconds* \| **msec**
>
> *hold-milliseconds*}.
>
> **Step 5.** (Optional) Establish GLBP authentication by using the
> command **glbp** instance-id **authentication**
>
> {**text** *text-password* \| **md5** {**key-chain** *key-chain* \|
>
> **key-string** *key-string*}}.
>
> ![](media/image23.jpg)GLBP Status
>
> The command **show glbp brief** shows high-level details of the GLBP
> group, including the interface, group, active AVG, standby AVG, and
> statuses of the AVFs.
>
> The command **show glbp** displays additional information, including
> the timers, preemption settings, and statuses for the AVG and AVFs for
> the GLBP group.
>
> ![](media/image24.png)
>
> GLBP Load Balancing
>
> GLBP supports three methods of load balancing traffic:
>
> • **Round robin -** Uses each virtual forwarder MAC address to
> sequentially reply for the virtual
>
> IP address. GLBP uses round robin as the default load-balancing
> method.
>
> • **Weighted -** Defines weights to each device in the GLBP group to
> define the ratio of load balancing between the devices. This allows
> for a larger weight to be assigned to bigger routers that can handle
> more traffic.
>
> • **Host dependent -** Uses the host MAC address to decide to which
> virtual forwarder MAC to redirect the packet. This method ensures that
> the host uses the same virtual MAC address as long as the number of
> virtual forwarders does not change within the group.
>
> The load-balancing method can be changed with the command **glbp**
> *instance-id* **load- balancing** {**host-dependent** \|
> **round-robin** \| **weighted**}. The weighted load-balancing method
> has the AVG direct traffic to the AVFs based on the percentage of
> weight a router has over the total weight of all GLBP routers. The
> weight can be set for a router with the
>
> command **glbp** *instance-id* **weighting** *weight*.
>
> ![](media/image25.png)Verifying GLBP Weighted Load Balancing
>
> The example shows that the load-balancing method has been changed to
> weighted and that the appropriate weight has been set for each AVF.
>
> Network Address Translation
>
> • In the early stages of the internet, large network blocks were
> assigned to
>
> organizations.
>
> • Network engineers started to realize that as more people connected
> to the internet, the
>
> IP address space would become exhausted.
>
> RFC 1918 established common network blocks that are non-globally
> routed networks. These address blocks provide large private network
> blocks for companies to connect their devices
>
> together, but private IP addressing doesn't exist on the internet. The
> private address blocks
>
> are as follows:
>
> 10.0.0.0/8 accommodates 16,777,216 hosts.
>
> 172.16.0.0/24 accommodates 1,048,576 hosts.
>
> 192.168.0.0/16 accommodates 65,536 hosts.
>
> NAT enables the internal IP network to appear as a publicly routed
> external network. A NAT device (typically a router or firewall)
> modifies the source or destination IP addresses in a packet's header
> as the packet is received on the outside or inside interface. NAT can
> be used in use cases other than just providing internet connectivity
> to private networks such as providing connectivity when a company buys
> another company, and the two companies have overlapping networks.
>
> NAT enables the internal IP network to appear as a publicly routed
> external network.
>
> A NAT device (typically a router or firewall) modifies the source or
> destination IP addresses
>
> in a packet's header as the packet is received on the outside or
> inside interface.
>
> NAT can be used in use cases other than just providing internet
> connectivity to private networks, such as providing connectivity when
> a company buys another company, and the two companies have overlapping
> networks.
>
> Most routers and switches perform NAT translation only with the IP
> header addressing and do not translate IP addresses within the payload
> (for example, DNS requests). Some firewalls can perform NAT within the
> payload for certain types of traffic.
>
> Here are four important terms related to NAT:
>
> • Inside local - The actual private IP address assigned to a device on
> the inside network(s).
>
> • Inside global - The public IP address that represents one or more
> inside local IP
>
> addresses to the outside.
>
> • Outside local - The IP address of an outside host as it appears to
> the inside network.
>
> The IP address does not have to be reachable by the outside but is
> considered private and must be reachable by the inside network.
>
> • Outside global - The public IP address assigned to a host on the
> outside network. This
>
> IP address must be reachable by the outside network.
>
> Three types of NAT commonly used today are as follows:
>
> • Static NAT - Provides a static one-to-one mapping of a local IP
> address to a global IP
>
> address.
>
> • Pooled NAT - Provides a dynamic one-to-one mapping of a local IP
> address to a global IP address. The global IP address is temporarily
> assigned to a local IP address. After a certain amount of idle NAT
> time, the global IP address is returned to the pool.
>
> • Port Address Translation (PAT) - Provides a dynamic many-to-one
> mapping of many local IP addresses to one global IP address. The NAT
> device translates the private IP address and port to a different
> global IP address and port. The port is unique from any other ports,
> which enables the NAT device to track the global IP address to local
> IP addresses based on the unique port mapping.
>
> NAT Example
>
> ![](media/image26.jpg)Figure 15-7 is used throughout this section to
> illustrate NAT.
>
> R5 performs the translation; its Gi0/0 interface (10.45.1.5) is the
> outside interface, and its Gi0/1 (10.56.1.5) interface is the inside
> interface. The other devices act as either clients or servers to
> demonstrate how NAT functions.
>
> ![](media/image27.jpg)NAT Example (Cont.)
>
> Example 15-25 shows the routing tables of R1, R5 and R7.
>
> • R1, R2, and R3 all have a static
>
> ![](media/image28.jpg)default route toward R4.
>
> • R4 has a static default route to R5.
>
> • R7, R8, and R9 all have a static default route to R6
>
> • R6 has a static default route to R5.
>
> • R5 has two static routes. One to the
>
> 10.123.4.0/24 network via R4 and the other to the 10.78.9.0/24 network
> via R6.
>
> NAT Example (Cont.)
>
> ![](media/image29.png)• Example 15-26 shows a traceroute from R1 to
> R7. The topology provides full connectivity between the outside hosts
> (R1, R2, and R3) and the
>
> inside hosts (R7, R8, and R9).
>
> ![](media/image30.png)• Example 15-27 shows a telnet connection from
> R7 to R1. The local IP address reflects R1 (10.123.4.1) and the remote
> address is R7 (10.78.9.7) No NAT has occurred for this Telnet session.
>
> Static NAT involves the translation of a global IP address to a local
> IP address, based on a static mapping of the global IP address to the
> local IP address.
>
> There are two types of static NAT:
>
> • **Inside static NAT** - involves the mapping of an inside local
> (private) IP address to an inside global (public) IP address.
>
> • **Outside static NAT** - involves the mapping of an outside global
> (public) IP address to an outside local (private) IP address.
>
> The steps for configuring inside static NAT are as follows:
>
> **Step 1**. Configure the outside interfaces by using the command **ip
> nat outside**.
>
> **Step 2.** Configure the inside interface with the command **ip nat
> inside**.
>
> **Step 3**. Configure the inside static NAT by using the command **ip
> nat inside source**
>
> **static** *inside-local-ip inside-global-ip***.**
>
> ![](media/image31.jpg)
>
> ![](media/image32.png)Identifying the Source with Inside Static
> NAT/NAT Translation Table
>
> With NAT configured, a telnet session with R1 is initiated. Viewing
> the TCP session on R1, the local address remains 10.123.4.1 but the
> remote address now reflects 10.45.1.7.
>
> ![](media/image33.png)The NAT translation table consists of static and
> dynamic entries. The NAT translation table is displayed with the
> command **show ip nat translations**.
>
> • The first entry is the dynamic entry correlating
>
> to the Telnet session.
>
> • The second entry is the inside static NAT entry that was configured.
>
> NAT Translation Steps
>
> The NAT translation follows these steps:
>
> ![](media/image34.jpg)**Step 1**. As traffic enters the Gi0/1
> interface on R5, R5 performs a route lookup for the destination IP
> address, which points out of its Gi0/0 interface. R1 is aware that the
> Gi0/0 interface is an outside NAT interface and that the Gi0/1
> interface is an inside NAT interface and therefore checks the NAT
> table for an entry.
>
> **Step 2.** Only the inside static NAT entry exists, so R5 creates a
> dynamic inside NAT entry with the packet's destination (10.123.4.1)
> for the outside local and outside global address.
>
> **Step 3.** R5 translates (that is, changes) the
>
> ![](media/image35.jpg)packet's source IP address from 10.78.9.7 to
>
> 10.45.1.7.
>
> **Step 4.** R1 registers the session as coming from 10.45.1.7 and then
> transmits a return packet. The packet is forwarded to R4 using the
> static default route, and R4 forwards the packet using the static
> default route.
>
> **Step 5.** As the packet enters on the Gi0/0 interface of R5, R5 is
> aware that the Gi0/0 interface is an outside NAT interface and checks
> the NAT table for an entry.
>
> ![](media/image36.jpg)**Step 6.** R5 correlates the packet's source
> and
>
> destination ports with the first NAT entry, as shown in Example 15-30,
> and knows to
>
> modify the packet's destination IP address
>
> from 10.45.1.7 to 10.78.9.7.
>
> **Step 7.** R5 routes the packet out the Gi0/1 interface toward R6.
>
> Connectivity from External Devices to the Inside Global IP Address
>
> ![](media/image37.png)In Example 15-31:
>
> • R2 establishes a Telnet session with R7, using the inside global IP
> address 10.45.1.7.
>
> • R5 simply creates a second dynamic entry for this new session.
>
> • From R7's perspective, it has
>
> connected with R2 (10.123.4.2).
>
> Outside Static NAT
>
> Outside static NAT involves the mapping of an outside global (public)
> IP address to an outside local (private) IP address. The steps for
> configuring outside static NAT are as follows:
>
> **Step 1**. Configure the outside interfaces by using the command **ip
> nat outside**.
>
> **Step 2.** Configure the inside interface with the command **ip nat
> inside**.
>
> **Step 3.** Configure the outside static NAT by using the command **ip
> nat outside source static** *outside-global-ip outside-local-ip
> \[**add-route**\]***.**
>
> ![](media/image38.png)
>
> Outside Static NAT Demonstration
>
> R6, R7, R8, or R9 could initiate a Telnet session with R2's IP address
> (10.123.4.2) and no NAT translation would occur. The same routers
> could initiate a Telnet session with the R2's outside local IP address
> 10.123.4.222; or R2 could initiate a session with any of the inside
> hosts (R6, R7, R8, or R9) to demonstrate the outside static NAT entry.
>
> ![](media/image39.png)Example 15-33 shows R2 establishing a Telnet
> session with R9 (10.78.9.9).
>
> • From R9's perspective, the connection came
>
> from 10.123.4.222.
>
> • At the same time, R8 initiated a Telnet session with the outside
> static NAT outside local IP address (10.123.4.222)
>
> • From R2's perspective, the source address is
>
> R8's 10.78.9.8 IP address.
>
> ![](media/image41.jpg)NAT Translation Table for Outside Static NAT
>
> Figure 15-9 shows the translation table of R5 for the outside static
> NAT entry of R2 for 10.123.4.222.
>
> Example 15-34 shows the NAT translation table of R5.
>
> There are three entries:
>
> • The first entry is the outside static NAT
>
> entry that was configured.
>
> • The second entry is the Telnet session launched from R8 to the
> 10.123.4.222
>
> ![](media/image42.png)IP address.
>
> • The third entry is the Telnet session launched from R2 to R9's IP
> address (10.78.9.9).
>
> A downfall to static NAT is the number of configurations entries that
> must be created on the NAT device. In addition, the number of global
> IP addresses must match the number of local IP addresses.
>
> Pooled NAT provides a more dynamic method of providing a one-to-one IP
> address mapping---but on a dynamic, as-needed basis.
>
> The dynamic NAT translation stays in the translation table until
> traffic flow from the local address to the global address has stopped
> and the timeout period (24 hours by default) has expired. The unused
> global IP address is then returned to the pool to be used again.
>
> Pooled NAT can operate as inside NAT or outside NAT.
>
> The steps for configuring inside pooled NAT are as follows:
>
> **Step 1**. Configure the outside interfaces by using the command **ip
> nat outside**.
>
> **Step 2.** Configure the inside interface with the command **ip nat
> inside**.
>
> **Step 3.** Specify which traffic to translate by using a standard or
> extended ACL referenced by number or name. Using a user-friendly name
> may be simplest from an operational support perspective
>
> **Step 4.** Define the global pool of IP addresses by using the
> command **ip nat pool** *nat- pool-name starting-ip ending-ip*
> **prefix-length** *prefix-length*.
>
> **Step 5.** Configure the inside pooled NAT by using the command **ip
> nat inside source list**
>
> *acl* **pool** *nat-pool-name***.**
>
> ![](media/image43.jpg)Example 15-35 uses a NAT pool with the IP
> addresses 10.45.1.10 and 10.45.1.11. A named ACL, ACL-NAT-CAPABLE,
> allows only packets sourced from the
>
> 10.78.9.0/24 network to be eligible for pooled NAT.
>
> ![](media/image44.jpg)In Example 15-35, R7 and R8
>
> ping R1 in order to generate traffic and build the dynamic inside NAT
> translations.
>
> ![](media/image45.png)![](media/image46.png)In Example 15-37, there
> are a total of four translations in the translation table of R5. Two
> of them are for the full flow and specify the protocol, inside global,
> inside local, outside local, and outside global IP addresses.
>
> In Example 15-38, R8 establishes a Telnet session with R2. R2 detects
> that the remote IP address of the session is
>
> 10.45.1.11. A second method of confirmation is to examine the NAT
> translation on R5, where there is a second dynamic translation entry
> for the full Telnet session.
>
> ![](media/image47.jpg)Failed NAT Pool Allocation/Reset NAT Pool
>
> A downfall to using pooled NAT is that when the pool is exhausted, no
> additional translation can occur until the global IP address is
> returned to the pool. Example
>
> 15-39 demonstrates this concept with NAT
>
> failing on R5 and packets being dropped.
>
> ![](media/image48.png)The default timeout for NAT translations is 24
> hours, but this can be changed with the command **ip nat translation
> timeout** *seconds*.
>
> The dynamic NAT translations can be cleared out with the command
> **clear ip nat translation** {*ip- address* \| \*}, This removes all
> existing translations and could interrupt traffic flow on active
> sessions as they might be assigned new global IP addresses.
>
> Pooled NAT translation has the limitation of ensuring that the number
> of global IP addresses is adequate to meet the needs of the local IP
> addresses.
>
> Port Address Translation (PAT) is an iteration of NAT that allows for
> a mapping of many local
>
> IP addresses to one global IP address.
>
> The NAT device maintains the state of translations by dynamically
> changing the source ports as a packet leaves the outside interface.
>
> Another term for PAT is NAT overload.
>
> The steps for configuring PAT are as follows:
>
> ![](media/image49.jpg)**Step 1**. Configure the outside interface by
> using the command **ip nat outside**.
>
> **Step 2.** Configure the inside interface with the
>
> command **ip nat inside**.
>
> **Step 3.** Specify which traffic can be translated by using a
> standard or extended ACL
>
> referenced by number or name.
>
> **Step 4.** Configure Port Address Translation by using the command
> **ip nat inside source list** *acl* {interface *interface-id* \| pool
> *nat-pool- name*} **overload**.
>
> Generating Traffic for PAT
>
> ![](media/image50.png)Now that PAT has been configured on R5, traffic
> can be generated for testing.
>
> ![](media/image51.png)
>
> ![](media/image52.jpg)NAT Translation Table With PAT
>
> Figure 15-10 shows R5's translation table
>
> after all the various flows have established.
>
> Example 15-43 shows R5's NAT translation table. By taking the ports
> from the TCP brief sessions on R2 and correlating them to R5's NAT
> translation table, you can identify which TCP session belongs to R7 or
> R8.
>
> Prepare for the Exam

> Command Reference for Chapter 15

![](media/image54.jpg)

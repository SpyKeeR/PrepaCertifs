![](media/image1.jpg)

> Chapter 22: Enterprise
>
> Network Architecture
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 22 Content
>
> **This chapter covers the following content:**
>
> • **Hierarchical LAN Design Model -** This section describes the
> hierarchical network design, which improves performance, simplifies
> design, increases scalability, and reduces troubleshooting time.
>
> • **Enterprise Network Architecture Options -** This section describes
> the different options available for deploying an enterprise campus
> architecture based on the hierarchical LAN design model.
>
> Hierarchical LAN Design Model
>
> • A hierarchical LAN design model divides the enterprise network
> architecture into
>
> modular layers.
>
> • Modular layers allow each layer to implement specific functions.
>
> • Modular layers can be replicated throughout the network providing
> scaling and a consistent deployment method.
>
> • Provides fault containment.
>
> • Provides the ability to put network components in place or take them
> out of service with no impact on the rest of the network.
>
> 3 Layer Design
>
> • **Access layer -** Gives endpoints and users direct access to the
> network.
>
> • **Distribution layer -** Provides an aggregation point for the
> access layer and acts as a services and control boundary between the
> access layer and the core layer.
>
> • **Core layer (also referred to as the backbone) -** Provides
> connections between distribution layers for large environments.

![](media/image2.jpg)

> **Figure 22-1** *Hierarchical LAN Design*
>
> Scalable Layer Design
>
> ![](media/image3.jpg)The number of layers needed depends on the
> characteristics of the network deployment site. As illustrated in
> Figure 22-2, a small campus in a single building might require only
> access and distribution layers, while a campus that spans multiple
> buildings will most likely require all three layers. The modularity of
> this design ensures that each layer will provide the same services and
> the same design methods.
>
> **Figure 22-2** *Modular Design Scalability*
>
> Access Layer
>
> The access layer, also commonly referred as the network edge, is where
> end- user devices or endpoints connect to the network.
>
> It provides high-bandwidth device connectivity using wired and
> wireless access technologies such as Gigabit Ethernet and 802.11n and
>
> 802.11ac wireless.
>
> ![](media/image4.jpg)**Figure 22-3** *Access Layer Connectivity*
>
> Access Layer (Cont.)
>
> • It can be segmented (for example, by using VLANs) so that different
> devices can be placed into different logical networks for performance,
> management, and security reasons.
>
> • In the hierarchical LAN design, the access layer switches are not
> interconnected to each other. Communication between endpoints on
> different access layer switches occurs through the distribution layer.
>
> • It plays a big role in ensuring that the network is protected from
> malicious attacks.
>
> This protection includes making sure the end users and endpoints
> connecting to the network are prevented from accessing services for
> which they are not authorized.
>
> • Quality of service (QoS) trust boundary and QoS mechanisms are
> typically enabled on this layer to ensure that QoS is provided
> end-to-end to satisfy the end user's quality of experience (QoE).
>
> • The primary function of the distribution layer is to aggregate
> access layer switches in a given building or campus.
>
> • The distribution layer provides a boundary between the Layer 2
> domain of
>
> the access layer and the core's Layer 3 domain.
>
> • This boundary provides two key functions for the LAN:
>
> • On the Layer 2 side, the distribution layer creates a boundary for
>
> Spanning Tree Protocol (STP), limiting propagation of Layer 2 faults.
>
> • On the Layer 3 side, the distribution layer provides a logical point
> to summarize IP routing information when it enters the core of the
> network. The summarization reduces IP routing tables for easier
> troubleshooting and reduces protocol overhead for faster recovery from
> failures.
>
> • The distribution switches need to be deployed in pairs for
> redundancy as displayed in Figure
>
> 22-4.
>
> • The distribution layer switch pairs should be interconnected to each
> other using either a Layer 2 or Layer 3 link.
>
> • When campus buildings are geographically dispersed, distribution
> layer switches can be located within the buildings in order to reduce
> the number of fiber-optic runs (which are costly) between buildings.
>
> ![](media/image5.jpg)**Figure 22-4** *Distribution Layer Connectivity*
>
> ![](media/image6.jpg)
>
> **Figure 22-5** *Distribution Layer Reducing Fiber Optic Runs*
>
> Core Layer
>
> • As networks grow beyond three distribution layers in a single
> location, organizations should consider using a core layer to optimize
> the design.
>
> • The core layer is the backbone and aggregation point for multiple
> networks and provides scalability, high availability, and fast
> convergence to the network.
>
> • The core can provide high-speed connectivity for large enterprises
> with multiple campus networks distributed worldwide, and it can also
> provide interconnectivity between the
>
> end-user/endpoint campus access layer and other network blocks, such
> as the data center, the private cloud, the public cloud, the WAN, the
> internet edge, and network services.

![](media/image7.jpg)

> **Figure 22-6** *Core Layer Reduces Large Network Complexity*
>
> Use of the core to reduce the network complexity, from
>
> N × (N − 1) to N links for N distribution layer switches.
>
> Enterprise Network
>
> Architecture Options
>
> • Two-tier design (collapsed core)
>
> • Three-tier design
>
> • Layer 2 access layer (STP based)
>
> • Layer 3 access layer (routed access)
>
> • Simplified campus design
>
> • Software-Defined Access (SD-Access)
>
> Two-tier design (Collapsed Core)
>
> • Smaller campus networks may have multiple departments spread across
> multiple floors within a building. In these environments, a core layer
> may not be needed, and collapsing the core function into the
> distribution layer can be a cost-effective solution (as no core layer
> means no core layer devices) that requires no sacrifice of most of the
> benefits of the three-tier hierarchical model.
>
> • Prior to selecting a two-tier collapsed core and distribution
> layers, future scale, expansion, and manageability factors need to be
> considered.
>
> Two-tier design (Cont.)
>
> Switches at the Core/Distribution layer provide two separate
> functions:
>
> • connectivity to the WAN, Data Center, internet, and network services
> edge blocks
>
> • LAN aggregation to the end-user access layer switches
>
> ![](media/image8.jpg)The WAN Edge block connects to remote data
> centers, remote branches, or other campus networks or for connectivity
> to cloud providers.
>
> The Data Center/Server Room block is where business-critical servers
> are placed.
>
> The Internet Edge block is used for regular internet access,
> e-commerce, connection to remote branches, remote VPN access and
> non-dedicated cloud provider connections.
>
> The Network Services block is where devices
>
> providing network services reside, such as wireless
>
> LAN controllers (WLCs).

**Figure 22-7** *Two-Tier/Collapsed Core Design*

> Three-Tier Design
>
> Three-tier designs separate the core and distribution layers and are
> recommended
>
> when more than two pairs of distribution switches are required.
>
> Multiple pairs of distribution switches are typically required for the
> following reasons:
>
> • When implementing a network for a large enterprise campus composed
> of
>
> multiple buildings, where each building requires a dedicated
> distribution layer.
>
> • When the density of WAN routers, internet edge devices, data center
> servers, and network services are growing to the point where they can
> affect network performance and throughput.
>
> • When geographic dispersion of the LAN access switches across many
> buildings in a larger campus facility would require more fiber-optic
> interconnects back to a single collapsed core.
>
> Three-Tier Design (Cont.)
>
> In Figure 22-8, the building blocks or places in the network (PINs)
> are each using the hierarchical design model.
>
> Each block is deployed with a pair of distribution switches connected
> to the core.
>
> The hierarchical LAN design is more appropriate for north--south
> traffic flows, such as endpoints communicating with the WAN edge, data
> center, Internet, or network services blocks.
>
> The data center block is using the newer leaf--spine design, an
> alternative to the three- tier design when traffic is predominantly
> east--west between servers within the data center.

![](media/image9.jpg)

> **Figure 22-8** *Three-Tier Design*
>
> Layer 2 Access Layer (STP Based)
>
> • Traditional LAN designs use a Layer 2 access layer and a Layer 3
> distribution
>
> layer.
>
> • The distribution layer is the Layer 3 IP gateway for access layer
> hosts.
>
> • Whenever possible, it is recommended to restrict a VLAN to a single
> access layer
>
> switch to eliminate topology loops.
>
> • Restricting a VLAN to a single switch provides a loop-free design,
> but at the cost of network flexibility because all hosts within a VLAN
> are restricted to a single access switch.
>
> • Some organizations require that the same Layer 2 VLAN be extended to
> multiple
>
> access layer switches to accommodate an application or a service.
>
> • The looped design causes STP to block links, which reduces the
> bandwidth from the rest of the network and can cause slower network
> convergence.
>
> Layer 2 Access Layer (STP Based) -- Topology Design
>
> ![](media/image10.jpg)Figure 22-9
>
> illustrates a loop-free topology where a VLAN is constrained to a
> single switch, as well as a looped topology where a VLAN spans
> multiple access switches.
>
> The looped design causes STP to block
>
> links. **Figure 22-9** *Loop-Free Topology and Looped Topology*
>
> Layer 2 Access Layer (STP Based) -- High Availability
>
> • First-hop redundancy protocols (FHRPs) provide hosts with a
> consistent MAC address and gateway IP address for each configured
> VLAN. The distribution layer should have a pair of standalone switches
> configured with a FHRP.
>
> • Hot Standby Router Protocol (HSRP) and Virtual Router Redundancy
> Protocol
>
> (VRRP) are the most common first-hop redundancy protocols.
>
> • The downside to these protocols is that they only allow hosts to
> send data out the
>
> active FHRP router through a single access uplink.
>
> • This leaves one of the access layer-to-distribution layer uplinks
> unutilized unless manual configuration of the distribution layer is
> performed.
>
> • Gateway Load Balancing Protocol (GLBP) provides greater uplink
> utilization for access layer-to-distribution layer traffic by load
> balancing the load from hosts across multiple uplinks.
>
> • The downside is that it works only on loop-free topologies.
>
> Routed access is an alternative configuration in which Layer 3 is
> extended all the way to the access layer switches. In this design,
> access layer switches act as full Layer 3 routed nodes (providing both
> Layer 2 and Layer 3 switching), and the access-to- distribution Layer
> 2 uplink trunks are replaced with Layer 3 point-to-point routed links.
> Consequently, the Layer 2/Layer 3 demarcation point is moved from the
> distribution switch to the access switch, as illustrated in Figure
> 22-10.
>
> ![](media/image11.jpg)
>
> **Figure 22-10** *Layer 2 Access Layer and Layer 3 Access Layer*
>
> The routed access-to-distribution block design advantages over the
> Layer 2 access layer design:
>
> • **No first-hop redundancy protocol required -** It eliminates the
> need for first-hop
>
> redundancy protocols such as HSRP and VRRP.
>
> • **No STP required -** Because there are no Layer 2 links to block,
> this design eliminates the need for STP.
>
> • **Increased uplink utilization -** Both uplinks from access to
> distribution can be used, increasing the effective bandwidth available
> to the end users and endpoints connected to the access layer switches.
>
> • **Easier troubleshooting -** It offers common end-to-end
> troubleshooting tools (such
>
> as **ping** and **traceroute**).
>
> • **Faster convergence -** It uses fast-converging routing protocols
> such as Enhanced
>
> Interior Gateway Routing Protocol (EIGRP) and Open Shortest Path First
> (OSPF).
>
> Relies on switch clustering such as a virtual switching system (VSS)
> and stacking technologies such as StackWise, in which multiple
> physical switches act as a single logical switch. Clustering and
> stacking technologies can be applied to any of the campus building
> blocks to simplify them even further. Using this design offers the
> following advantages:
>
> • **Simplified design -** By using the single logical distribution
> layer design, there are fewer boxes to manage, which reduces the
> amount of time spent on ongoing provisioning and maintenance.
>
> • **No first-hop redundancy protocol required -** It eliminates the
> need for first-hop redundancy protocols such as HSRP and VRRP because
> the default IP gateway is on a single logical interface.
>
> • **Reduced STP dependence -** Because EtherChannel is used, it
> eliminates the need for STP for a Layer 2 access design. However, STP
> is still required as a failsafe in case multiple access switches are
> interconnected.
>
> Simplified Campus Design advantages:
>
> • **Increased uplink utilization -** With EtherChannel, all uplinks
> from access to distribution can be used, increasing the effective
> bandwidth available to the end users and endpoints connected to the
> access layer switches.
>
> • **Easier troubleshooting -** The topology of the network from the
> distribution layer to the access layer is logically a hub-and-spoke
> topology, which reduces the complexity of the design and
> troubleshooting.
>
> • **Faster convergence -** With EtherChannel, all links are in
> forwarding state, and this significantly optimizes the convergence
> time following a node or link failure event. Provides fast sub-second
> failover between links in an uplink bundle.
>
> • **Distributed VLANs -** With this design, VLANs can span multiple
> access switches
>
> without the need to block any links.
>
> The simplified campus design is loop free, highly available, flexible,
> resilient, and easy to manage. Figure 22-11 illustrates how the
> network can be simplified by introducing VSS and StackWise into the
> design.
>
> ![](media/image12.jpg)
>
> **Figure 22-11** *Simplified Campus Design with VSS and StackWise*
>
> Using the simplified campus design approach across all the campus
> blocks (when possible) can provide an optimized architecture that is
> easy to manage, resilient, and more flexible, with higher aggregated
> uplink bandwidth capacity.

![](media/image13.jpg)

> **Figure 22-12** *Applying VSS and StackWise in a Campus Network*
>
> SD-Access - Industry's first intent-based networking solution for the
> enterprise
>
> • Built on the principles of the Cisco Digital Network Architecture
> (DNA)
>
> • A combination of the campus fabric design and the Digital Network
>
> Architecture Center (Cisco DNA or DNAC).
>
> • Adds fabric capabilities to the enterprise network through
> automation
>
> • Provides automated end-to-end segmentation to separate user, device,
> and application traffic without requiring a network redesign
>
> • Fabric capabilities provide services such as host mobility and
> enhanced
>
> security in addition to the normal switching and routing capabilities.
>
> Prepare for the Exam

![](media/image14.jpg)

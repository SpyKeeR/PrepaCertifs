![](media/image1.jpg)

> Chapter 10: OSPFv3
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 10 Content
>
> **This chapter covers the following content:**
>
> **OSPFv3 Fundamentals:** This section provides an overview of the
> OSPFv3 routing protocol and the similarities to OSPFv2.
>
> **OSPFv3 Configurations:** This section demonstrates the configuration
> and verification of an OSPFv3 environment.
>
> **IPv4 Support in OSPFv3:** This section explains and demonstrates how
>
> OSPFv3 can be used for exchanging IPv4 routes.
>
> OSPFv3 Fundamentals
>
> • OSPFv3 supports IPv4 and IPv6 address families.
>
> • New LSA types have been created to carry IPv6 prefixes.
>
> • The IP prefix information is carried as LSA payload information,
> making the protocol essentially address family independent.
>
> • Includes a new link-state type field that is used to determine the
> flooding scope of LSA, as well as the handling of unknown LSA types.
>
> • OSPFv3 runs directly over IPv6, and the number of fields in the
> packet header has been reduced.
>
> Features
>
> • **Router ID -** The router ID is used to identify neighbors,
> regardless of the network type in OSPFv3. The router ID must always be
> manually assigned in the routing process.
>
> • **Authentication -** Neighbor authentication has been removed from
> the OSPF protocol and is now performed through IPsec extension headers
> in the IPv6 packet.
>
> • **Neighbor adjacencies -** OSPFv3 inter-router communication is
> handled by
>
> IPv6 link-local addressing.
>
> • **Multiple subnets on an interface -** Allows for neighbor adjacency
> to form even if the two routers do not share a common subnet.
>
> • **Multiple instances -** OSPFv3 packets include an instance ID field
> that may be used to manipulate which routers on a network segment are
> allowed to form adjacencies.
>
> • OSPFv3 packets use protocol ID 89.
>
> • Routers communicate with each other using the link-local address.
>
> • OSPFv3 modifies the structure of the router LSA (type 1).
>
> • It renames the network summary LSA to the interarea prefix LSA.
>
> • It renames the ASBR summary LSA to the interarea router LSA.
>
> • Router LSA is responsible for announcing interface parameters such
> as the interface
>
> type and metric.
>
> • IP address information is advertised independently by two new LSA
> types:
>
> • Intra-area prefix LSA
>
> • Link-local LSA
>
> • Link-state database(LSDB) creates a shortest path topology tree
> based on links instead of networks. Since IP address information is
> advertised using new LSA types there is no longer a need to run SPF
> calculations every time a new address prefix is added or changed on an
> interface.

> Table 10-2 OSPFv3 LSA Types

© 2016 Cisco and/or its affiliates. All rights reserved. Cisco
Confidential 6

> OSPFv3 Communication
>
> Destination address is either a unicast link-local address or a
> multicast link-local scoped
>
> address:
>
> **FF02::05: OSPFv3 AllSPFRouters**
>
> Every router uses AllSPFRouters multicast address to send OSPF hello
> messages to routers on the same link.
>
> Hello messages are used for neighbor discovery and detecting whether a
> neighbor relationship is down.
>
> DR and BDR routers also use this address to send link-state update and
> flooding acknowledgment messages to all routers.
>
> **FF02::06: OSPFv3 AllDRouters designated router (DR)**
>
> Non-DR/BDR routers send an update or link-state acknowledgment message
> to the DR and BDR by using the AllDRouters.
>
> OSPFv3 uses the same five packet types and logic as OSPFv2.
>
> **OSPFv3 Packet Types**
>
> **Table 10-3** OSPFv3 Packet Types

> OSPFv3 Configurations
>
> Configuration Steps:
>
> • Step 1. Initialize the routing process with the command \'ipv6
> unicast-routing\'.
>
> • Step 2. Define the 32-bit router ID within the OSPFv3 router
> process.
>
> • Step 3. (Optional) Initialize the address family - enabled
> automatically when OSPFv3 is enabled on an interface.
>
> • Step 4. Enable OSPFv3 on an interface using a process-id and
> area-id.
>
> OSPFv3 Topology
>
> Figure 10-1 displays a simple four-router topology to demonstrate
> OSPFv3
>
> configuration.
>
> Area 0 consists of R1, R2, and R3, and Area 34 contains R3 and R4. R3
> is the ABR.
>
> ![](media/image2.jpg)
>
> Example OSPFv3 Configuration
>
> Earlier versions of IOS used the commands **ipv6 router ospf** for
> initialization of the OSPF process and **ipv6 ospf *process-id* area
> *area-id ***for identification of the interface. These commands are
> considered legacy and should be migrated to the current practice such
> as **ospfv3 *process-id* ipv6 area *area-id ***in the R1 & R2
> configurations, as highlighted below.
>
> ![](media/image3.jpg)

![](media/image4.png)© 2016 Cisco and/or its affiliates. All rights
reserved. Cisco Confidential 11

> **Example OSPFv3 Configuration (Cont.)**
>
> **R3 & R4 configurations steps are highlighted below.**
>
> R3
>
> interface .LoopbackO
>
> ipv6 address 2001:DBB::3/12B
>
> ospfv3 1 ipv6 area 0
>
> interface GigabitEthernet0/2
>
> ipv6 address FBB0::3 link-local ipv6 address 2001:DBB:0:23::3/64
> ospfv3 1 ipv6 area 0
>
> interface GigabitEthernet0/4
>
> ipv6 address FBB0::3 link-local ipv6 address 2001:DBB:0:34::3/64
> ospfv3 1 ipv6 area 34
>
> router ospfv3 1
>
> router-id 192.168.3.3

R4

> interface LoopbackO
>
> ipv6 address 2001:DBB::4/12B
>
> ospfvJ 1 ipv6 area 34
>
> interface GigabitEthernet0/1
>
> ipv6 address FEBO::4 link-local ipv6 address 200l:DBB:0:4::4/64 ospfv3
> 1 ipv6 area 34
>
> interface GigabitEthernet0/3
>
> ipv6 address FEBO::4 link-local ipv6 address 2001:DBB:0:34::4/64
> ospfvJ 1 ipv6 area 34

router ospfv3 1

> router-id 192.168.4.4
>
> OSPFv3 Verification -- Neighbor Adjacency
>
> To view the R3 OSPFv3 Neighbor Adjacency the **show opsfv3 ipv6
> neighbor**
>
> command is used.
>
> Neighbors router-id is displayed, OSPFv3 priority, state of the
> connection, and the interface the neighbor is learned on.
>
> ![](media/image5.jpg)
>
> OSPFv3 Verification
>
> ![](media/image6.jpg)Verifying the OSPFv3 interface information
> provides the following:
>
> • Interface ID
>
> • Router ID
>
> • DR and Backup DR
>
> • Neighbor Adjacency
>
> To show a brief listing of the interfaces participating in OSPFv3
> Routing on R3 use the **show ospfv3 interface brief** command.
>
> Important information includes the Interface, the area the interface
> belongs to, and the
>
> role of the router on the link (State)
>
> ![](media/image8.jpg)
>
> OSPFv3 Routing Verification
>
> ![](media/image9.png)Output from the OSPFv3 routing table showing both
> Intra-Area routes (O) and Inter-Area routes (OI) using the command
> **show ipv6 route ospf.**
>
> OSPFv3 Passive Interface
>
> OSPFv3 supports marking an interface as passive. The command is placed
> under the OSPFv3 process or under the specific address family. Placing
> the command under the global process cascades the setting to both
> address families.
>
> • The passive interface can be set explicitly to an interface (R1
> configuration).
>
> • The passive interface can be set as default (R4 configuration).
>
> ![](media/image10.jpg)
>
> OSPFv3 Route Summarization
>
> ![](media/image11.png)Example 10-9 shows the summarization commands
> applied to R3.
>
> ![](media/image12.png)Route summarization reduces the number of route
> entries on the neighboring router as shown in examples 10-8 and 10-10.
>
> ![](media/image13.png)
>
> OSPFv3 Verify Network Type
>
> ![](media/image14.jpg)Configuration changes may be necessary for a
> dynamically learned network type. As shown in Example 10-11 the R2
> G0/3 interface is shown as a BROADCAST network type.
>
> Based on the topology it should be a point-to-point.
>
> ![](media/image15.jpg)
>
> ![](media/image16.jpg)OSPFv3 Change Network Type
>
> When changes are made to the network type it is necessary to change
> both ends of the link to match. The change is made directly on the
> interface.
>
> IPv4 Support in OSPFv3
>
> Enabling IPv4 Support
>
> • Step 1. Ensure that the IPv4 interface has an IPv6 address (global
> or link local)
>
> configured.
>
> • Step 2. Enable the OSPFv3 process for IPv4 on the interface with the
> command
>
> **ospfv3** *process-id* **ipv4 area** *area-id*.
>
> IPv4 Support in OSPFv3
>
> Adding IPv4 support to existing interfaces
>
> Using the command **ospfv3 *process-id* ipv4 area *area-id ***on an
> interface configured for
>
> ![](media/image18.png)IPv6 adds IPv4 support. The interface must have
> an IPv6 global or link-local address.
>
> ![](media/image19.png)
>
> 1Pv4 Support in OSPFv3
>
> Verifying 1 Pv4 Routes
>
> Verifying OSPFv3 routes for 1Pv4 is accomplished using the command
> show ip route ospfv3.
>
> Example 10-15 *Verifying IPv4 Route Exchange with OSPFv3*
>
> R4# ohow ip route ospfv3 1 begin Gatewa.y
>
> Gateway of last resort is not set
>
> 10.0.0.0/S is variably subnetted, 5 subnets, 2 masks
>
> 0 IA 10.1.1.0/24 \[110/4\] via 10.34.1.3, 00:00:39, GigabitEthernet0/3
>
> 0 IA 10.12.1.0/24 \[110/3\]via 10.34.1.3, 00:00:39, GigabitEtbernet0/3
>
> 0 IA 10.23.1.0/24 \[110/2\] via 10.34.1.3, 00:00:39,
> GigabitEthernet0/3
>
> 192.168.. 1.0/32 is subnetted, 1 subnets
>
> 0 IA 192.169.1.1 \[110/3\] via 10.34.1.3, 00:00:39, GigabitEthernet0/3
>
> 192.168.2.0/32 is subnetted, 1 subnets
>
> IPv4 Support in OSPFv3
>
> Displaying OSPFv3 Interfaces
>
> To display the interfaces configured for OSPFv3 and the respective
> address family use the command **show ospfv3 interface brief.**
>
> ![](media/image20.jpg)

© 2016 Cisco and/or its affiliates. All rights reserved. Cisco
Confidential 24

> **1Pv4 Support in OSPFv3**
>
> **Verifying OSPFv3 Neighbors**
>
> **To verify the OSPFv3 neighbors for bath 1Pv4 and 1Pv6 use the
> command show ospfv3 neighbor.**
>
> **E xample 10-17** *Venfying OS PFv3 !Pv4 Neighbors*
>
> R4 \# ohow oopfv3 ne, ighbor
>
> OSPFv3 1 address-family ipv4 {router-id 192.168.4.4)

> OSPFv3 1 address-family ipv6 {router-id 192.168.4.4)

> Prepare for the Exam

![](media/image21.jpg)

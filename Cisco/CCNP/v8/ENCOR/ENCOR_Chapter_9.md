![](media/image1.png)

> Chapter 9: Advanced OSPF
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 9 Content
>
> **This chapter covers the following content:**
>
> • **Areas -** This section describes the benefits and functions of
> areas within an Open Shortest Path First
>
> (OSPF) routing domain.
>
> • **Link-State Announcements -** This section explains how OSPF
> stores, communicates, and builds a topology from the link-state
> announcements (LSAs).
>
> • **Discontiguous Networks -** This section demonstrates a
> discontiguous network and explains why such a network cannot
> distribute routes to all areas properly.
>
> • **OSPF Path Selection -** This section explains how OSPF makes path
> selection choices for routes learned within the OSPF routing domain.
>
> • **Summarization of Routes -** This section explains how network
> summarization works with OSPF.
>
> • **Route Filtering -** This section explains how OSPF routes can be
> filtered on a router.
>
> The (OSPF) protocol scales well with proper network planning. IP
> addressing schemes, area segmentation, address summarization, and
> hardware capabilities for each area should considered when designing a
> network.
>
> Areas
>
> • An OSPF area is a logical grouping of routers or, more specifically,
> a logical grouping of router interfaces.
>
> • Area membership is set at the interface level, and the area ID is
> included in the OSPF
>
> hello packet.
>
> • An interface can belong to only one area.
>
> • All routers within the same OSPF area maintain an identical copy of
> the link-state database (LSDB).
>
> OSPF Areas
>
> An OSPF area grows in size as the number of network links and routers
> increase in the area. While using a single area simplifies the
> topology, there are trade-offs:
>
> • Full shortest path first (SPF) tree calculation runs when a link
> flaps within the area.
>
> • The LSDB increases in size and becomes unmanageable.
>
> • The LSDB for the area grows, consuming more memory, and lengthening
> the SPF
>
> computation process.
>
> • No summarization of route information occurs.
>
> Proper design addresses each of these issues by segmenting the routers
> into multiple OSPF areas, thereby keeping the LSDB to a manageable
> size. Sizing and design of OSPF networks should account for the
> hardware constraints of the smallest router in that area.
>
> OSPF Areas (Cont.)
>
> In essence, an OSPF area hides the topology from another area but
> enables the networks to be visible in other areas within the OSPF
> domain. Segmenting the OSPF domain into multiple areas reduces the
> size of the LSDB for each area, making SPF tree calculations faster,
> and decreasing LSDB flooding between routers when a link flaps.
>
> ![](media/image2.png)Just because a router connects to multiple OSPF
> areas does not mean the routes from one area will be injected into
> another area. Figure 9-1 shows router R1 connected to Area 1 and Area
> 2. Routes from Area 1 will not advertise into Area 2 and vice versa.
>
> OSPF Area 0 and ABRs
>
> Area 0 is a special area called the backbone. By design, all areas
> must connect to Area 0 because OSPF expects all areas to inject
> routing information into the backbone, and Area 0 advertises the
> routes into other areas.
>
> Area border routers (ABRs) are OSPF routers connected to Area 0 and
> another OSPF area. ABRs are responsible for advertising routes from
> one area and injecting them into a different OSPF area.
>
> ![](media/image3.png)
>
> Figure 9-2 shows that R1 is connected to Area 0, Area 1, and Area 2.
> R1 is a proper ABR because it now participates in Area 0.
>
> Multi-Area OSPF Configurations and Verifying Interfaces for ABRs
>
> ![](media/image4.png)
>
> Figure 9-3 shows a larger-scale OSPF multi- area topology. In the
> topology:
>
> • R1, R2, R3, and R4 belong to Area 1234.
>
> • R4 and R5 belong to Area 0.
>
> • R5 and R6 belong to Area 56.
>
> • R4 and R5 are ABRs.
>
> • Area 1234 connects to Area 0, and Area
>
> 56 connects to Area 0.
>
> • Routers in Area 1234 can see routes from routers in Area 0 and Area
> 56 and vice versa.
>
> ![](media/image5.png)Example 9-1 shows the OSPF configuration for the
> ABRs R4 and R5.

![](media/image6.png)

> Example 9-2 verifies that interfaces on R4 belong to Area 1234 and
>
> Area 0 and that interfaces on R5 belong to Area 0 and Area 56.
>
> Area ID
>
> • The area ID is a 32-bit field and can be formatted in simple decimal
> (0 through
>
> 4,294,967,295) or dotted decimal (0.0.0.0 through 255.255.255.255).
>
> • During router configuration, the area can use decimal format on one
> router and dotted-decimal format on a different router, and the
> routers can still form an adjacency.
>
> • OSPF advertises the area ID in dotted-decimal format in the OSPF
> hello packet.
>
> OSPF Intra-Area and Interarea Routes
>
> ![](media/image7.png)Network routes that are learned from other OSPF
> routers within the same area are known as intra-area routes. In Figure
> 9-3, the network link between R2 and R4 (10.24.1.0/29) is an intra-
> area route to R1. The IP routing table displays OSPF intra-area routes
> with an O.
>
> ![](media/image8.png)Network routes that are learned from other OSPF
> routers from a different area using an ABR are known as interarea
> routes.
>
> Example 9-3 provides the routing table for R1 from Figure 9-3. Notice
> that R1's OSPF routing table shows routes from within Area 1234 as
> intra-area (O routes) and routes from Area 0 and Area 56 as interarea
> (O IA routes).

i li l

![](media/image9.png)

> In Example 9-4, notice that R4's routing table shows the routes from
> within Area 1234 and Area 0 as intra-area and routes from Area 56 as
> interarea because R4 does not connect to Area 56. The metric for the
> 10.123.1.0/24 and 10.3.3.0/24 networks has drastically increased
> compared to the metric for the 10.56.1.0/24 network.
>
> ![](media/image11.png)
>
> ![](media/image12.png)Example 9-5 provides the routing tables with
> filtering for OSPF for R5 and R6.
>
> Figure 9-3. R5 and R6 only contain interarea routes in the OSPF
> routing table because intra-area routes are directly connected.
>
> External routes are routes learned from outside the OSPF domain but
> injected into an OSPF domain through redistribution. External OSPF
> routes can come from a different OSPF domain or from a different
> routing protocol.
>
> Link-State Announcements
>
> • When OSPF neighbors become adjacent, the LSDBs synchronize between
> the OSPF
>
> routers.
>
> • As an OSPF router adds or removes a directly connected network link
> to or from its database, the router floods the link-state
> advertisement (LSA) out all active OSPF interfaces.
>
> • The OSPF LSA contains a complete list of networks advertised from
> that router.
>
> OSPF LSA Types for IPv4 Routing
>
> OSPF uses six LSA types for IPv4 routing:
>
> • **Type 1, router LSA -** Advertises the LSAs that originate within
> an area.
>
> • **Type 2, network LSA -** Advertises a multi-access network segment
> attached to a DR.
>
> • **Type 3, summary LSA -** Advertises network prefixes originating
> from a different area.
>
> • **Type 4, ASBR summary LSA -** Advertises a summary LSA for a
> specific ASBR.
>
> • **Type 5, AS external LSA -** Advertises LSAs for routes that have
> been redistributed.
>
> • **Type 7, NSSA external LSA -** Advertises redistributed routes in
> NSSAs.
>
> LSA types 1, 2, and 3, which are used for building the SPF tree for
> intra-area and interarea routes, are explained in this section.
>
> Components of the LSA
>
> Components of the LSA include the LSA type, LSA age, sequence number,
> and advertising router.
>
> • **LSA age and flooding**: Every OSPF LSA includes an age that is
> entered into the local LSDB and that will increment by 1 every second.
> When a router's OSPF LSA age exceeds 1800 seconds (30 minutes) for its
> networks, the originating router advertises a new LSA with the LSA age
> set to 0. The LSA is deemed invalid if age reaches 3600.
>
> ![](media/image13.jpg)• **LSA sequences**: OSPF uses the sequence
> number to overcome problems caused by delays in LSA propagation in a
> network. The LSA sequence number is a 32-bit number for controlling
> versioning.
>
> • **LSA types**: All routers within an OSPF area have an identical set
> of LSAs for that area. The ABRs maintain a separate set of LSAs for
> each OSPF area.
>
> ![](media/image14.png)LSA Type 1: Router Link
>
> Every OSPF router advertises a type 1 LSA. Type 1 LSAs are the
> essential building blocks within the LSDB. A type 1 LSA entry exists
> for each OSPF-enabled link. Type 1 LSAs for an area are shown with the
> command **show ip ospf database router**.
>
> Figure 9-5 shows that in this example, the type 1 LSAs are not
> advertised outside Area 1234, which means the underlying topology in
> an area is invisible to other areas.
>
> The initial fields of each type 1 LSA indicate the RID for the LSA's
> advertising router, age, sequence, link count, and link ID. Every
> OSPF- enabled interface is listed under the number of links for each
> router.

© 2016 Cisco and/or its affiliates. All rights reserved. Cisco
Confidential 15

> LSA Type 2: Network Link
>
> ![](media/image15.jpg)A type 2 LSA represents a multi-access network
> segment that uses a DR. The DR always advertises the type 2 LSA and
> identifies all the routers attached to that network segment. If a DR
> has not been elected, a type 2 LSA is not present in the LSDB because
> the corresponding type 1 transit link type LSA is a stub. Like type 1
> LSAs, type 2 LSAs are not flooded outside the originating OSPF area.
>
> Detailed type 2
>
> LSA information is shown with the command
>
> **show ip ospf database network**.
>
> LSA Type 3: Summary Link
>
> ![](media/image16.png)Type 3 LSAs represent networks from other areas.
> The role of the ABRs is to participate in multiple OSPF areas and
> ensure that the networks associated with type 1 LSAs are reachable in
> the non-originating OSPF areas. Figure 9-9 demonstrates the concept of
> a type 3 LSA interaction with type 1 LSAs.
>
> The advertising router for type 3 LSAs is the last ABR that advertises
> the prefix. The metric within the type 3 LSA uses the following logic:
>
> • If the type 3 LSA is created from a type 1 LSA, it is the total path
> metric to reach the originating router in the type 1 LSA.
>
> • If the type 3 LSA is created from a type 3 LSA from Area 0, it is
> the total path metric to the ABR
>
> plus the metric in the original type 3 LSA.
>
> ![](media/image17.png)The type 3 LSA contains the link-state ID
> (network number), the subnet mask, the IP address of the advertising
> ABR, and the metric for the network prefix.
>
> Figure 9-10 provides R4's perspective of the type 3 LSA created by ABR
> (R5) for the
>
> 10.56.1.0/24 network. The total path metric to 10.56.1.0/24 is 2.
>
> Figure 9-11 provides R3's perspective of the type 3 LSA created by ABR
> (R4) for the 10.56.1.0/24 network.
>
> • R3 does not know if the 10.56.1.0/24 network is directly attached to
> the ABR (R4) or multiple hops away.
>
> • R3 knows that its metric to the ABR (R4) is 65 and that the type 3
> LSA already has a metric of
>
> 2, so its total path metric to reach the 10.56.1.0/24 network is 67.
>
> ![](media/image18.png)
>
> Discontiguous Networks
>
> • This section will cover an example of a discontiguous network.
>
> • The simplest fix for a discontiguous network is to ensure that Area
> 0 is contiguous.
>
> An OSPF network with this design is discontiguous because interarea
> traffic is trying to cross a nonbackbone area.
>
> It looks like routes in the routing tables on R2 and R3 in Figure 9-13
> are being advertised across area 23. The 10.34.1.0/24 network was
> advertised into OSPF by R3 and R4 as a type 1
>
> LSA. R3 is an ABR and converts Area 34's
>
> 10.34.1.0/24 type 1 LSA into a type 3 LSA in Area 0. R3 uses the type
> 3 LSA from Area 0 to generate the type 3 LSA for Area 23. R2 is able
> to install the type 3 LSA from Area 23 into its routing table.

![](media/image19.png)

> **Note**: To assume that the 10.34.1.0/24 route learned by Area 23
> would then advertise into R2's Area 0 and then propagate to Area 12,
> would be wrong.
>
> There are three fundamental rules ABRs use the for creating type 3
> LSAs:
>
> • Type 1 LSAs received from an area create type 3 LSAs into the
> backbone area and nonbackbone areas.
>
> • Type 3 LSAs received from Area 0 are created for the nonbackbone
> area.
>
> • Type 3 LSAs received from a nonbackbone area only insert into the
> LSDB for the source area. ABRs do not create a type 3 LSA for the
> other areas (including a segmented Area 0).
>
> The simplest fix for a discontiguous network is to ensure that Area 0
> is contiguous. There are other functions, like virtual link or usage
> of GRE tunnels that are not covered in this course.
>
> Real-life scenarios of discontiguous networks involve Area 0 becoming
> partitioned due to hardware failures.
>
> OSPF Path Selection
>
> • OSPF executes Dijkstra's shortest path first (SPF) algorithm to
> create a loop-free topology of shortest paths.
>
> • All routers use the same logic to calculate the shortest path for
> each network.
>
> • Path selection prioritizes paths by using the following logic:
> intra-area, interarea, and external routes (which involves additional
> logic and not covered here)
>
> Intra-Area Routes
>
> Routes advertised via a type 1 LSA for an area are always preferred
> over type 3 LSAs. If
>
> ![](media/image20.png)multiple intra-area routes exist, the path with
> the lowest total path metric is installed in the OSPF Routing
> Information Base (RIB), which is then presented to the router's global
> RIB. If there is a tie in metric, both routes install into the OSPF
> RIB.
>
> In Figure 9-14, R1 is computing the route to 10.4.4.0/24. Instead of
> taking the faster Ethernet connection, R1 takes the path across the
> slower serial
>
> link to R4 because that is the intra-area path.
>
> ![](media/image21.png)In Example 9-6, notice that the metric is 111
> and that the intra-area path was selected over the interarea path with
> the lower total path metric.
>
> Interarea Routes and Equal Cost Multipathing
>
> The next priority for selecting a path to a network is selection of
> the path with the lowest total path metric to the destination. If
> there is a tie in metric, both routes install into the OSPF RIB. All
> interarea paths for a route must go through Area 0 to be considered.
>
> ![](media/image22.png)In Figure 9-15, R1 is computing the path to R6.
> R1 uses the path R1--R3--R5--R6 because its total path metric is 35
> versus the R1--R2--R4--R6 path, with a metric of 40.
>
> If OSPF identifies multiple paths in the path selection algorithms,
> those routes are installed into the routing table as equal-cost
> multipathing (ECMP) routes. The default maximum number of ECMP paths
> is four paths.
>
> Summarization of Routes
>
> • Route scalability is a large factor for the IGP routing protocols
> used by service providers because there can be thousands of routers
> running in a network.
>
> • Splitting up an OSPF routing domain into multiple areas reduces the
> size of the LSDB for each area.
>
> • While the number of routers and networks remains the same within the
> OSPF routing domain, the detailed type 1 and type 2 LSAs are exchanged
> for simpler type 3 LSAs.
>
> ![](media/image23.png)Summarization of Routes Example
>
> • Referencing our topology for LSAs, in Figure 9-16 for Area 1234,
> there are three type 1 LSAs and one type 2
>
> LSA for the 10.123.1.0/24 network.
>
> • Those four LSAs become one type 3
>
> LSA outside Area 1234.
>
> • This illustrates the reduction of LSAs through area segmentation for
> the
>
> 10.123.1.0/24 network.
>
> Summarization Fundamentals
>
> • Another method of shrinking the LSDB involves summarizing network
> prefixes. An OSPF
>
> area needs to accommodate the smallest and slowest router in that
> area.
>
> • Summarization of routes also helps SPF calculations run faster.
> Because all routers within an area must maintain an identical copy of
> the LSDB, summarization occurs between areas on the ABRs.
>
> • Summarization can eliminate the SPF calculation outside the area for
> the summarized prefixes because the smaller prefixes are hidden.
>
> Figure 9-17 provides a simple network topology where the serial link
> between R3 and R4 adds to the path metric, and all traffic uses the
> other path to reach the 172.16.46.0/24 network. If the 10.1.12.0/24
> link fails, all routers in Area 1 have to run SPF calculations. R4
> identifies that the 10.1.13.0/24 and
>
> 10.1.34.0/24 networks will change their next hop through the serial
> link. Both of the type 3 LSAs for these networks need to be updated
> with new path metrics and advertised into Area 0. The routers in Area
> 0 run an SPF calculation only on those two prefixes.
>
> ![](media/image24.png)
>
> Figure 9-18 shows the networks in Area 1 being summarized at the ABR
> into the aggregate 10.1.0.0/18 prefix. If the 10.1.12.0/24 link fails,
> all the routers in Area 1 still run the SPF calculation, but routers
> in Area 0 are not impacted because the 10.1.13.0/24 and 10.1.34.0/24
> networks are not known outside Area 1.
>
> ![](media/image25.png)
>
> Interarea Summarization
>
> • Interarea summarization reduces the number of type 3
>
> LSAs that an ABR advertises into an area when it receives type 1 LSAs.
>
> • The network summarization range is associated with a specific source
> area for type 1 LSAs.
>
> • When a type 1 LSA within the summarization range reaches the ABR
> from the source area, the ABR creates a type 3 LSA for the summarized
> network range.
>
> • The ABR suppresses the more specific type 3 LSAs, thereby preventing
> the generation of the subordinate route's type 3 LSAs. Interarea
> summarization does not impact the type 1 LSAs in the source area.
>
> Summarization works only on type 1 LSAs and is normally configured so
> that summarization occurs as routes enter the backbone from
> nonbackbone areas.

![](media/image26.png)

> Figure 9-19 shows 15 type 1 LSAs (172.16.1.0/24 through
> 172.16.15.0/24) being summarized into one type 3 LSA (the
> 172.16.0.0/20 network).
>
> Summarization of Routes
>
> Summarization Metrics
>
> The default metric for the summary LSA is the smallest metric
> associated with an LSA. However, it can be set as part of the
> configuration.
>
> OSPF behaves identically to Enhanced Interior Gateway Routing Protocol
> (EIGRP) and checks every prefix within the summarization range when a
> matching type 1 LSA is added or removed. If a lower metric is
> available, the summary LSA is advertised with the newer metric; if the
> lowest metric is removed, a newer and higher metric is identified, and
> a new summary LSA is advertised with the higher metric.

![](media/image27.png)

> In Figure 9-20, R1 summarizes three prefixes with various path costs.
>
> Configuration of Interarea Metrics
>
> ![](media/image28.png)• To define the summarization range and
> associated area, use the command **area** *area-id* **range** *network
> subnet-mask* \[**advertise \| not-advertise**\] \[**cost** *metric*\]
> under the OSPF process on the ABR.
>
> • The default behavior is to advertise the summary prefix, so the
> keyword **advertise** is not necessary.
>
> • Appending the cost metric keyword to the
>
> ![](media/image29.png)command statically sets the metric on the
> summary route.
>
> Figure 9-21 provides a topology example in which R1 is advertising the
> 172.16.1.0/24,
>
> 172.16.2.0/24, and 172.16.3.0/24 networks.

Example 9-7 displays the routing table on R3 before summarization.
Notice that the

172.16.1.0/24, 172.16.2.0/24, and 172.16.3.0/24 networks are all
present.

> ![](media/image30.png)Example 9-8 provides R2's configuration for
> interarea summarization into an aggregate route of 172.16.0.0/16. A
> static cost of 45 is added to the summary route to reduce CPU load if
> any of the three networks flap.
>
> ![](media/image31.png)Example 9-9 displays R3's routing table for
> verification that the smaller routes were suppressed while the summary
> route was aggregated. Notice that the path metric is 46, whereas
> previously the metric for the
>
> 172.16.1.0/24 network was 3.
>
> The ABR performing interarea summarization installs a discard route.
> The discard route is a route to the Null0 interface that matches the
> summarized network range. Discard routes prevent routing
>
> loops where portions of the summarized network range do not have a
> more specific route in the RIB. The AD for the OSPF summary discard
> route for internal networks is 110, and it is 254 for external
> networks.
>
> Example 9-10 shows the discard route on R2 for the 172.16.0.0/16
> prefix.
>
> ![](media/image32.png)
>
> Route Filtering
>
> • Route filtering is a method for selectively identifying routes that
> are advertised or received from neighbor routers.
>
> • Route filtering may be used to manipulate traffic flows, reduce
> memory utilization, or improve security.
>
> • Filtering of routes with vector-based routing protocols is
> straightforward as the routes are filtered as routing updates are
> advertised to downstream neighbors.
>
> • With link-state routing protocols such as OSPF, every router in an
> area shares a complete copy of the linkstate database. Therefore,
> filtering of routes generally occurs as routes enter the area on the
> ABR.
>
> Filtering with Summarization
>
> One of the easiest methodologies for filtering routes is to use the
> **not-advertise** keyword during prefix summarization. This prevents
> creation of any type 3 LSAs for any networks in that range, thus
> making the subordinate routes visible only within the area where the
> route originates.
>
> The full command structure is **area** *area-id* **range** *network
> subnet-mask* **not-advertise** under the
>
> ![](media/image33.png)OSPF process.
>
> In the configuration in 9-11 we see that R2 can filter out any of the
> type
>
> 1 LSAs that are generated in Area
>
> ![](media/image34.png)12 from being advertised into Area 0.
>
> Example 9-12 shows R3's routing table after the area filtering
> configuration has been placed on R2.
>
> Area Filtering
>
> Although filtering via summarization is very easy, it is limited in
> its ability. For example, in Figure 9-
>
> 22, if the 172.16.1.0/24 network needs to be present in Area 0 but
> removed in Area 34, it is not possible to filter the route using
> summarization.
>
> ![](media/image35.png)
>
> ![](media/image36.png)![](media/image37.png)Other network designs
> require filtering of OSPF routes based on other criteria. OSPF
> supports filtering when type 3 LSA generation occurs, allowing for the
> original route to be installed in the LSDB for the source area so that
> the route can be installed in the RIB of the ABR. Filtering can occur
> in either direction on the ABR. Figure 9-23 demonstrates the concept.
>
> Figure 9-24 expands on the
>
> sample topology and demonstrates that the ABR can filter routes as
> they advertise out of an area or
>
> into an area.

![](media/image38.png)

> OSPF area filtering is accomplished by using the command **area**
>
> *area-id* **filter-list prefix** *prefix-list-name* {**in \| out**} on
> the ABR. Example 9-13 provides a configuration for R2 and R3.

i li l

> Local OSPF Filtering
>
> In some scenarios, routes need to be removed only on specific routers
> in an area. OSPF is a link- state protocol that requires all routers
> in the same area to maintain an identical copy of the LSDB for that
> area. A route can exist in the OSPF LSDB, but it could be prevented
> from being installed
>
> in the local RIB. This is accomplished by using a Distribute List.
>
> Figure 9-25 illustrates this concept.
>
> ![](media/image40.png)

© 2016 Cisco and/or its affiliates. All rights reserved. Cisco
Confidential 41

> ![](media/image41.png)Configuring the OSPF Distribute List
>
> A distribute list is configured under the OSPF
>
> process with the command **distribute-list**
>
> {*acl-number* \| *acl-name* \| **prefix** *prefix-list- name* \|
> **route-map** *route-map-name*} **in**.
>
> Example 9-16 shows the routing tables for R2 and R3. The 172.16.3.0/24
> network is removed from R2's RIB but is present on R3's RIB.

i li l 42

> Prepare for the Exam

> **Task Command Syntax**
>
> Initialize the OSPF process **router ospf** *process-id*
>
> Summarize routes as they are crossing an OSPF ABR
>
> Filter routes as they are crossing an
>
> OSPF ABR

**area** *area-id* **range network subnet-mask**

\[**advertise \| not-advertise**\] \[**cost** *metric***\]**

**area** *area-id* **filter-list prefix** *prefix-list-name*

{**in \| out**}

> Filter OSPF routes from entering the RIB **distribute-list**
> {*acl-number* **\|** *acl-name* **\| prefix** *prefix-list-name* **\|
> route-map** *route-map-name*} **in**
>
> Display the LSAs in the LSDB **show ip ospf database** \[**router \|
> network \|**
>
> **summary**\]

![](media/image43.png)

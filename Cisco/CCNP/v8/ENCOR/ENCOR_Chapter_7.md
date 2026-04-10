![](media/image1.jpg)

> Chapter 7: EIGRP
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 7 Content
>
> **This chapter covers the following content:**
>
> • **EIGRP Fundamentals -** This section explains how EIGRP establishes
> a neighbor adjacency with other routers and how routes are exchanged
> with other routers.
>
> • **Path Metric Calculation -** This section explains how EIGRP
> calculates the path metric to identify the best and alternate
> loop-free paths.
>
> • **Failure Detection and Timers -** This section explains how EIGRP
>
> detects the absence of a neighbor and the convergence process.
>
> • **Route Summarization -** This section explains the logic and
> configuration related to summarizing routes on a router.
>
> EIGRP Fundamentals
>
> • EIGRP overcomes the deficiencies of other distance vector routing
> protocols with unequal-cost load balancing, support for networks 255
> hops away, and rapid convergence features.
>
> • EIGRP uses a diffusing update algorithm (DUAL) to identify network
> paths and enable
>
> fast convergence using precalculated loop-free backup paths.
>
> • EIGRP adds to the route selection algorithm logic that uses factors
> outside hop count.
>
> A router can run multiple EIGRP processes. Each process operates under
> the context of an autonomous system, which represents a common routing
> domain. Routers within the same domain use the same metric calculation
> formula and exchange routes only with members of the same autonomous
> system, as shown in the figure.
>
> ![](media/image2.png)

> ![](media/image3.jpg)

> ![](media/image4.jpg)

![](media/image5.jpg)

> EIGRP contains a topology table that makes it different from a "true"
> distance vector routing protocol. EIGRP's topology table is part of
> DUAL and helps to identify loop-free backup routes. It contains all
> the network prefixes advertised within an EIGRP autonomous system.
>
> Each entry in the table contains the following:
>
> • Network prefix
>
> • EIGRP neighbors that have advertised that prefix
>
> • Metrics from each neighbor (for example, reported distance, hop
> count)
>
> • Values used for calculating the metric (for example, load,
> reliability, total delay,
>
> minimum bandwidth)

![](media/image6.png)

> The show topology command will display both successor and feasible
> successors.
>
> EIGRP Neighbors
>
> EIGRP neighbors exchange the entire routing table when forming an
> adjacency, and they advertise only incremental updates as topology
> changes occur within a network. EIGRP uses five different packet types
> to communicate with other routers.

> Table 7-3 EIGRP Packet Types
>
> Path Metric Calculation
>
> • Metric calculation is a critical component for any routing protocol.
> EIGRP uses multiple factors to calculate the metric for a path.
>
> Metric calculation uses bandwidth and delay by default, but it can
> include interface load and reliability, too. The formula shown in
> Figure 7-4 illustrates the EIGRP classic metric formula.
>
> ![](media/image7.png)
>
> • EIGRP uses K values to define which factors the formula uses and the
> associated
>
> impact of a factor when calculating the metric.
>
> • BW represents the slowest link in the path scaled to a 10 Gbps link.
> Link speed is collected from the configured interface bandwidth on an
> interface.
>
> • Delay is the total measure of delay in the path, measured in tens of
> microseconds (μs).
>
> • The EIGRP formula is based on the IGRP metric formula, except the
> output is multiplied by 256 to change the metric from 24 bits to 32
> bits.
>
> ![](media/image8.png)
>
> By default, K1 and K3 have the value 1, and K2, K4, and K5 are set to
> 0.
>
> Figure 7-6 places default K values into the formula and then shows a
> streamlined
>
> version of the formula.
>
> ![](media/image9.png)
>
> EIGRP Attribute Propagation
>
> • The EIGRP update packet includes path attributes associated with
> each prefix.
>
> • The EIGRP path attributes can include hop count, cumulative delay,
> minimum bandwidth link
>
> speed, and RD.
>
> • The attributes are updated each hop along the way, allowing each
> router to independently identify the shortest path.
>
> ![](media/image10.png)
>
> Default EIGRP Interface Metrics for Classic Metrics

> ![](media/image11.png)**Table 7.4** Default EIGRP Interface Metrics
> for Classic Metrics
>
> Wide Metrics
>
> The original EIGRP specifications measured delay in 10 μs units and
> bandwidth in kilobytes per
>
> second, which did not scale well with higher-speed interfaces.
>
> Example 7-1 provides some metric calculations for common LAN interface
> speeds. Notice that there is not a differentiation between an 11 Gbps
> interface and a 20 Gbps interface. The composite metric stays at 256,
> despite having different bandwidth rates.

**Example 7.1** Calculating Metrics for Common LAN Interface Speeds

> EIGRP includes support for a second set of metrics, known as wide
> metrics, that addresses the issue of scalability with higher-capacity
> interfaces. Figure 7-9 shows the explicit EIGRP wide metrics formula.
>
> Notice that an additional K value (K6) is included that adds an
> extended attribute to measure jitter, energy, or other future
> attributes.
>
> ![](media/image12.png)
>
> EIGRP wide metrics scale by 65,535 to accommodate higher-speed links.
> This provides
>
> support for interface speeds up to 655 Tbps (65,535 × 107 ) without
> any scalability
>
> issues.
>
> Figure 7-10 displays the updated formula that takes into account the
> conversions in latency and scalability.
>
> ![](media/image13.png)
>
> With EIGRP wide metrics, K1 and K3 are set to a value of 1, and K2,
> K4, K5, and K6 are set to 0, which allows backward compatibility
> because the K value metrics match with classic metrics.
>
> EIGRP is able to detect when peering with a router is using classic
> metrics, and it unscales a metric from the formula in Figure 7-11.
>
> ![](media/image14.png)
>
> Load Balancing
>
> Installing multiple paths into the RIB for the same prefix is called
> equal-cost multipathing (ECMP*)*. EIGRP supports unequal-cost load
> balancing by changing EIGRP's variance multiplier. The
>
> EIGRP variance value is the feasible distance (FD) for a route
> multiplied by the EIGRP variance multiplier. Any feasible successor's
> FD with a metric below the EIGRP variance value is installed into the
> RIB.
>
> Dividing the feasible successor metric by the successor route metric
> provides the variance
>
> ![](media/image15.png)multiplier. The variance multiplier is a whole
> number, so any remainders should always round up.
>
> Load Balancing (Cont.)
>
> ![](media/image16.jpg)Verify unequal load balancing with the
>
> **show ip route** command.
>
> Failure Detection and
>
> Timers
>
> • A secondary function for the EIGRP hello packets is to ensure that
> EIGRP neighbors are still healthy and available. EIGRP hello packets
> are sent out in intervals determined by the hello timer.
>
> • EIGRP uses a second timer for the hold time, which is the amount of
> time EIGRP deems the router reachable and functioning. If the hold
> time reaches 0, EIGRP declares the neighbor unreachable and notifies
> DUAL of a topology change.
>
> • The default EIGRP hello timer is 5 seconds, but it is 60 seconds on
> slow-speed
>
> interfaces (T1 or lower). The hold time value defaults to 3 times the
> hello interval.
>
> Convergence
>
> When an EIGRP neighbor moves to a down state, paths are recomputed for
> any prefix where
>
> that EIGRP neighbor was a successor (upstream router).
>
> ![](media/image17.jpg)When EIGRP detects that it has lost its
> successor for a path, the feasible successor instantly becomes the
> successor route. The router sends out an update packet for that path
> because of the new EIGRP path metrics. Downstream routers run their
> own DUAL for any impacted prefixes to account for the new EIGRP
> metrics. Figure 7-13 demonstrates such a scenario when the link
> between R1 and R3 fails.
>
> If a feasible successor is not available for a prefix, DUAL must
> perform a new route calculation. The route state changes from passive
> (P) to active (A) in the EIGRP topology table.
>
> The router detecting the topology change sends out query packets to
> EIGRP neighbors for the route. The query packet includes the network
> prefix with the delay set to infinity so that other routers are aware
> that it has gone active.
>
> Upon receipt of a query packet, an EIGRP router does one of the
> following:
>
> • It might reply to the query that the router does not have a route to
> the prefix.
>
> • If the query did not come from the successor for that route, it
> detects the delay set for infinity but ignores it because it did not
> come from the successor. The receiving router replies with the EIGRP
> attributes for that route.
>
> • If the query came from the successor for the route, the receiving
> router detects the delay set for infinity, sets the prefix as active
> in the EIGRP topology, and sends out a query packet to all downstream
> EIGRP neighbors for that route.
>
> The query process continues from router to router until a router
> establishes the query boundary. A query boundary is established when a
> router does not mark the prefix as active, meaning that it responds to
> a query as follows:
>
> • It says it does not have a route to the prefix.
>
> • It replies with EIGRP attributes because the query did not come from
> the successor.
>
> ![](media/image18.jpg)When a router receives a reply for every
> downstream query that was sent out, it completes the DUAL, changes the
> route to passive, and sends a reply packet to any upstream routers
> that sent a query packet to it. Figure 7-14 shows a topology where the
> link between R1 and R2 has failed.
>
> Route Summarization
>
> • Scalability of an EIGRP autonomous system depends on summarization.
> As the size of an EIGRP autonomous system increases, convergence may
> take longer. Scaling an EIGRP topology requires summarizing routes in
> a hierarchical fashion.
>
> Route Summarization
>
> EIGRP Summarization
>
> EIGRP summarizes network prefixes on an interface basis. A summary
> aggregate is configured for the EIGRP interface. Prefixes within the
> summary aggregate are suppressed, and the summary aggregate prefix is
> advertised in lieu of the original prefixes. The summary aggregate
> prefix is not advertised until a prefix matches it. Interface-specific
> summarization can be performed in any portion of the network topology.
>
> ![](media/image19.jpg)
>
> Prepare for the Exam

![](media/image20.jpg)

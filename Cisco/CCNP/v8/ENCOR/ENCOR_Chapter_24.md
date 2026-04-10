![](media/image1.jpg)

> Chapter 24: Network Assurance
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 24 Content
>
> **This chapter covers the following content:**
>
> • **Network Diagnostic Tools -** This section covers the common use
> cases and operations of ping, traceroute, SNMP, and syslog.
>
> • **Debugging -** This section describes the value of using debugging
> as a troubleshooting tool and provides basic configuration examples.
>
> • **NetFlow and Flexible NetFlow -** This section examines the
> benefits and operations of
>
> NetFlow and Flexible NetFlow.
>
> • **Switched Port Analyzer (SPAN Technologies) -** This section
> examines the benefits and operations of SPAN, RSPAN, and ERSPAN.
>
> • **IP SLA -** This section covers IP SLA and the value of automated
> network probes and monitoring.
>
> • **Cisco DNA Center Assurance -** This section provides a high-level
> overview of Cisco DNA Center Assurance and associated workflows for
> troubleshooting and diagnostics.
>
> Network Diagnostic Tools
>
> Many network diagnostic tools are readily available. This section
> covers some of the most common tools available and provides use cases
> and examples of when to use them.
>
> Ping
>
> Ping is one of the most useful troubleshooting.
>
> The following troubleshooting flow is a quick way to check
> reachability and try to determine what the issue may be:
>
> **Step 1.** Gather the facts.
>
> **Step 2.** Test reachability by using the **ping** command.
>
> **Step 3.** Record the outcome of the **ping** command and move to the
> next troubleshooting step. If **ping** is successful, then the issue
> isn't likely related to basic reachability. If **ping** is
> unsuccessful, the next step could be checking something more advanced,
> such as interface issues, routing issues, access lists, or
> intermediate firewalls.
>
> Successful and Unsuccessful Pings
>
> Example 24-1 illustrates a successful ping between R1 and R2. This
> example shows five 100- byte ICMP echo request packets sent to
> 10.1.12.2 with a 2-second timeout. The result is five exclamation
> points (!!!!!).
>
> ![](media/image2.jpg)
>
> It is important to illustrate what an unsuccessful ping looks like as
> well. Example 24-2 shows
>
> an unsuccessful ping to R2's Ethernet0/0 interface with an IP address
> of 10.1.12.2.
>
> ![](media/image3.png)
>
> Ping Options
>
> The ping command can be changed and manipulated to aid in
> troubleshooting. Example 24-3 shows some of the available options for
> the **ping** command on a Cisco device. These options can be seen by
> using the context sensitive help (?) after the IP address that follows
> the ping command. This section specifically focuses on the **repeat**,
> **size**, and **source** options.
>
> ![](media/image4.png)
>
> Ping Size
>
> Another very common use case for the **ping** command is to send
> different sizes of packets to a destination. An example might be to
> send 1500-byte packets with the DF bit set to make sure there are no
> MTU issues on the interfaces or to test different quality of service
> policies that restrict certain packet sizes. Example 24-5 shows a ping
> destined to R2's Ethernet0/0 interface with an IP address 10.1.12.2
> and a packet size of 1500 bytes.
>
> ![](media/image5.jpg)
>
> An extended ping can take advantage of the same options already
> discussed, as well as some more detailed options for troubleshooting.
> These options are listed in Table 24-2.

> ![](media/image6.png)Setting the MTU in an extended ping and setting
> the DF bit in the IP header can help determine whether there are MTU
> settings in the path that are not set appropriately.
>
> With tunneling it is important to account for the overhead of the
> tunnel technology, which can vary. Specifying a Type of Service of 184
> in decimal translates to Expedited Forwarding or (EF) per-hop behavior
> (PHB). This can be useful when testing real-time quality of service
> (QoS) policies.
>
> Setting Data Patterns can help when troubleshooting framing errors,
> line coding, or clock signaling issues on serial interfaces.
>
> Finally, a timestamp is set in this example, in addition to the
> default Verbose output. This gives a clock timestamp of when the
> destination sent an echo reply message back to the source.
>
> Traceroute
>
> **Traceroute** is often used to troubleshoot when trying to determine
> where traffic is failing as well as what path traffic takes
> through-out the network.
>
> **Traceroute** shows the IP addresses or DNS names of the hops between
> the source and destination.
>
> ![](media/image7.jpg)It also shows how long it takes to reach the
> destination at each hop, measured in milliseconds. This tool is
> frequently used when more than one path is available to the
> destination or when there is more than one hop to the destination.
>
> ![](media/image8.jpg)Adding a Less Specific Route
>
> A less specific route is added to R1 that points to 22.0.0.0/8 or
> 22.0.0.0
>
> 255.0.0.0, the traceroute returns a "host unreachable" message. This
> is because there is a route to the next hop, R2 (10.1.12.2), but once
> the traceroute gets to R2, there is no interface or route to
> 22.22.22.23/32, and the traceroute fails. Example
>
> 24-11 shows this scenario.
>
> Traceroute Options
>
> Another benefit of **traceroute** is that it has options available.
> These options can also be discovered by leveraging the
> context-sensitive help (?) from the command-line interface. Example
> 24-14 shows the list of available options to the traceroute command.
>
> ![](media/image9.jpg)
>
> There are times when using some of the options available with
> **traceroute** may be . There are also times when there might be a
> reason to send a different number of probes per hop with different
> timeout timers rather than the default of three probes.
>
> Extended Traceroute Options
>
> Much like the extended **ping** command covered earlier in this
> chapter, there is an extended **traceroute** command, and it has a
> number of detailed options available. Those options are listed in
> Table 24-3.

> Debugging
>
> • Debugging can be a very powerful part of troubleshooting complex
> issues in a network.
>
> • One of the most common use cases for debugging is when there is a
> need to see things at a deeper level (such as when routing protocols
> are having adjacency issues).
>
> • There is a normal flow that is taken from a troubleshooting
> perspective, depending on
>
> the routing protocol.
>
> Debugging Topology
>
> ![](media/image10.jpg)Using the simple topology shown in Figure 24-2,
> in this section, debugging is used to fix a couple issues in the OSPF
> area 0.
>
> OSPF Adjacency Issues
>
> Some of the common OSPF adjacency issues such as MTU issues, incorrect
> interface types, and improperly configured network mask can be
> resolved by using debugging.
>
> ![](media/image11.png)From the output of the **show ip ospf neighbor**
> command on R1 in Example 24-17, it can be seen that the neighbor
> adjacency to R4 is in the INIT state. If the command is run after a
> few seconds, the state changes to EXCHANGE but quickly cycles back to
> the INIT state when the command is run again.
>
> Debugging is used on R1 to try to determine what the issue is. Example
> 24-18 shows the output of the **debug ip ospf adj** command. This
> command is used to reveal messages that are exchanged during the OSPF
> adjacency process.
>
> The output of the debug ip ospf adj command in Example 24-18 clearly
> states that it received a Database Descriptor packet from the neighbor
> 4.4.4.4, and that the neighbor
>
> 4.4.4.4 has a smaller interface MTU of 1400.

![](media/image12.jpg)© 2016 Cisco and/or its affiliates. All rights
reserved. Cisco Confidential 19

> Example 24-19 shows the output of the **debug ip ospf adj** command on
> R4 with the relevant fields highlighted. The output shows that R1 has
> an MTU size of 1500, which is larger than the locally configured MTU
> of 1400 on R4. This is a really quick way of troubleshooting this type
> of issue with adjacency formation
>
> ![](media/image13.jpg)
>
> Output of the Debug IP OSPF Hello Command
>
> ![](media/image14.png)The issue with OSPF network type mismatch, which
> is a very common reason for neighbor adjacency issues. Often this is
> simply a misconfiguration issue when setting up the network.
>
> When the **debug ip ospf hello** command is used on R1, everything
> appears to be normal: Hellos are sent to the multicast group 224.0.0.5
> every
>
> 10 seconds.
>
> Example 24-20 shows the output of
>
> the **debug** command on R1.
>
> Output of the Debug IP OSPF Hello Command (Cont.)
>
> Example 24-21 shows the issue output on R4.
>
> Based on the output, we can see that the hello parameters are
> mismatched. The output
>
> shows that R4 is receiving a dead interval of 40, while it has a
> configured dead interval of
>
> 120\. We can also see that the hello interval R4 is receiving is 10,
> and the configured hello interval is 30. By default, the dead interval
> is 4 times the hello interval.
>
> ![](media/image15.png)
>
> Different network types have different hello intervals and dead
> intervals. Table 24-4 high- lights the different hello and dead
> interval times based on the different OSPF network types.
>
> Table 24-4 OSPF Network Types and Hello/Dead Intervals

![](media/image16.jpg)

> The issue could be simply mismatched network types or mismatched hello
> or dead intervals.
>
> The **show ip ospf interface** command shows what the configured
> network types and hello and dead intervals are.
>
> Example 24-22 shows the output of this command on R4.
>
> Changing the Network Type
>
> Simply changing the network type on R4 interface Ethernet0/1 back to
> the default of Broadcast fixes the adjacency issue in this case. This
> is because R1 is configured as Broadcast, and now the hello and dead
> intervals will match.
>
> ![](media/image17.jpg)Example 24-23 shows the **ip ospf network-type
> broadcast** command issued to change the network type to Broadcast on
> the Ethernet0/1 interface and the neighbor adjacency coming up. It is
> also verified with the do **show ip ospf neighbor** command.
>
> Show and Debug Commands on R1
>
> ![](media/image19.jpg)The final use case for using debugging to solve
> OSPF adjacency issues involves improper configuration of IP addresses
> and subnet masks on an OSPF interface.
>
> To troubleshoot this without having to look through running
> configurations or at a specific interface, use the **debug ip ospf
> hello** command covered earlier in this section.
>
> Example 24-24 shows the output of running the **show ip ospf
> neighbor** command on R1. It indicates that there is no OSPF adjacency
> to R4 when there certainly should be one.
>
> Ping
>
> The network mask on the Ethernet0/1 interface of R4 needs to be
> changed to match the
>
> one that R1 has configured and is sending to R4 through OSPF hellos.
>
> ![](media/image20.jpg)Example 24-26 shows the network mask being
> changed on the R4 Ethernet0/1 interface and the OSPF adjacency coming
> up. This is then verified with the **do show ip ospf neighbor**
> command.
>
> Conditional debugging can be used to limit the scope of the messages
> that are being returned to the console or syslog server. A great
> example of this is the **debug ip packet** command. Issuing this
> command on a router that is in production could send back a tremendous
> number of messages.
>
> One way to alleviate this issue is to attach an access list to the
> **debug** command to limit the scope of messages to the source or
> destination specified within the access list. This can be done using
> standard or extended access lists.
>
> The options for the **debug ip packet** command are as follows:
>
> • **\<1-199\>**: Standard access list
>
> • **\<1300-2699\>**: Access list with expanded range
>
> • **detail**: More debugging detail
>
> Another common method of conditional debugging is to debug on a
> specific interface. This is extremely useful when trying to narrow
> down a packet flow between two hosts.
>
> Imagine that a network engineer is trying to debug a traffic flow
> between R1's Ethernet0/1 interface with source IP address
> 192.168.14.1/24 that is destined to R4's Loopback0 interface with IP
> address 4.4.4.4/32.
>
> One way to do this would certainly be to change the access list 100 to
> reflect these source and destination IP addresses. However, because
> the access list is looking for any traffic sourced or destined to the
> 192.168.14.0/24 network, this traffic flow would fall into matching
> that access list. Using conditional debugging on the Loopback0
> interface of R4 would be a simple way of meeting these requirements.
>
> Even if all debugging has been turned off using the undebug all
> command, the interface conditions set for Loopback0 on R4 remain. The
> way to remove this condition is to use the undebug interface loopback0
> command on R4.
>
> The typical tool for reactive alerting from network devices is Simple
> Network Management
>
> Protocol (SNMP).
>
> SNMP sends unsolicited traps to an SNMP collector or network
> management system
>
> (NMS). These traps are in response to something that happened in the
> network.
>
> For example, traps may be generated for link status events, improper
> user authentication, and power supply failures. These events are
> defined in the SNMP Management Information Base (MIB).
>
> The MIB can be thought of as a repository of device parameters that
> can be used to trigger alerts.
>
> There are currently three versions of SNMP. Table 24-5 lists the
> versions and their differences.
>
> Table 24-5 SNMP Version Comparison

> Using SNMP is considered best practice in production. SNMPv1 and
> SNMPv2c use access lists and a community password or string.
>
> These community strings can be read-
>
> only (RO) or read/write (RW). It is critical
>
> to limit SNMP access to these devices by using access lists.
>
> By default, if no version is specified in configuration, SNMPv1 is
> used. However, to better show how SNMP works, this chapter focuses on
> SNMPv2c.
>
> MIBs
>
> It is important to look at a MIB to understand some of the information
> or values that can
>
> be polled or send traps from SNMP.
>
> The SNMPv2-MIB.my file shows what values can be polled in the MIB and
> to illustrate sending traps from SNMP. To see a list of available
> Cisco MIBs, visit
> [[https://mibs.cloudapps.cisco.com/ITDIT/MIB]{.underline}
> [S/servlet/index]{.underline}.](https://mibs.cloudapps.cisco.com/ITDIT/MIBS/servlet/index)
>
> Although configuring an NMS is not covered in this chapter, the device
> side that points to an NMS is covered in this section.

The following list shows a handful of measures involved in setting up
SNMP on a device to allow the device to be polled and send traps to an
NMS:

> • Define the SNMP host or the NMS to send traps to

• Create an access list to restrict access via

> SNMP

• Define the read-only community string

• Define the read/write community string

• Define the SNMP location

• Define the SNMP contact

> MIBs (Cont.)
>
> These settings do not need to be configured in any particular order.
> It is best practice to configure the access list first and then the
> read-only and read/write strings to have security in place.
>
> On R1, a standard access list is configured to only permit access from
> an NMS host on the
>
> 192.168.14.0/24 subnet, 192.168.14.100. Once the access list is
> configured, the read-only and
>
> read/write community strings are configured and bound to that access
> list.
>
> ![](media/image22.png)It is important to try to use SNMP strings that
> are not easy to guess from a security perspective.
>
> At this point, the device is configured to be polled from an NMS host
> with the IP address
>
> 192.168.14.100.
>
> SNMP Traps
>
> To send SNMP traps to an NMS, traps first must be enabled on the
> device. All available traps can be enabled by issuing the
> **snmp-server enable traps** command.
>
> • However, this may enable unnecessary traps that have no significance
> to the network operations team. It might be more appropriate to be
> selective about which traps to enable.
>
> • The traps that are available to be enabled is platform specific.
>
> • A common approach to determining what traps are available is to look
> at the documentation for the device. It may be easier to simply issue
> the **snmp-server enable traps** command followed by **?** to leverage
> the context-sensitive help and determine what traps are available on
> the device.
>
> A significant number of traps can be enabled to send to an NMS.
>
> Syslog
>
> Devices can generate useful information to the console, to the logging
> buffer, and to off-box syslog collectors. In fact, all three can be
> sent the same or different message types.
>
> It is critical to note that prior to configuring any device to send
> log information, the date and time of the
>
> clock must be properly configured for accurate time.

> Syslog (Cont.)
>
> Having syslog configured doesn't mean that an issue will be found. It
> still takes the proper skill to
>
> be able to look at the messages and determine the root cause of the
> issue.
>
> The logging buffer is the first area to focus on. You can enable
> logging to the buffer as follows:
>
> 1\. Enable logging to the buffer.
>
> 2\. Set the severity level of syslog messages to send to the buffer.
>
> 3\. Set the logging buffer to a larger size.
>
> The **logging buffered ?** command is issued from the global
> configuration mode to see the available options. It is important to
> note that the severity level can be configured by simply specifying
> the level with a number from 0 to 7 or the name of the severity
> (listed next to the severity level number).
>
> The default size of the logging buffer is 4096 bytes. This can get
> overwritten quite quickly. It is
>
> good practice to expand the buffer size so you can capture more
> logging information.
>
> ![](media/image23.jpg)Logging Buffer Size and Severity Level
>
> Debugging or severity 7 is the level that will be configured in this
> example; with this configuration, any debugging can be sent to the
> logging buffer instead of the console.
>
> In Example 24-34, the logging is configured to the debugging level, 7,
> and it is set to 100000 bytes.
>
> Sending Logging to a Host for Debugging
>
> Sending these same logs to an off-box collector, that could be
> configured as well. By default, these messages are sent to the logging
> host through UDP port 514, but this can be changed if necessary.
>
> Configuring logging to a host is very similar to configuring logging
> on the console or buffer. In this case, it is configured by using the
> following steps:
>
> **1**. Enable logging to host 192.168.14.100.
>
> **2**. Set the severity level of syslog messages to send to host.
>
> Syslog can be used to notify of power supply failures, CPU spikes, and
> a variety of other things.
>
> It is important not to underestimate the level of granularity and
> detail that can be achieved by setting up proper notification policies
> in a network. It is ultimately up to the network operations team to
> determine how deep is appropriate to meet the business's needs.
>
> NetFlow and Flexible NetFlow
>
> • Gathering statistical information on traffic flows is necessary for
> a number of reasons.
>
> • NetFlow is very versatile and provides a wealth of information
> without much
>
> configuration burden.
>
> • NetFlow has two components that must be configured: NetFlow Data
> Capture and
>
> NetFlow Data Export.
>
> NetFlow Ingress/Egress Collected Traffic Types
>
> NetFlow captures traffic on ingress and egress---that is, traffic that
> is coming into the devices as well as traffic that is leaving them.
>
> NetFlow collects traffic based on flows. A flow is a unidirectional
> traffic stream that
>
> contains a combination of the following key fields:
>
> • Source IP address
>
> • Destination IP address
>
> • Source port number
>
> • Destination port number
>
> • Layer 3 protocol type
>
> • Type of service (ToS)
>
> • Input logical interface
>
> Enable NetFlow
>
> R1's Ethernet0/1 interface for NetFlow Data Capture and exporting the
> data to the
>
> 192.168.14.100 collector. Example 24-37 illustrates the process of
> configuring NetFlow
>
> Data Capture and NetFlow Data Export on R1.
>
> ![](media/image24.png)
>
> To verify that NetFlow and NetFlow Data Export were configured
> properly, a few commands can be run. The first is **show ip flow
> interface**, which shows the interfaces that are configured for
> NetFlow. The second is **show ip flow**, which shows the destination
>
> for the NetFlow data to be exported to. Finally, **show ip cache
> flow** shows the traffic flows that NetFlow is capturing.
>
> Configuring and Verifying the Top Talkers on R1
>
> ![](media/image25.jpg)NetFlow is able to configure the top specified
> number of talkers on the network.
>
> A very useful and quick configuration allows you to gain a great
> snapshot of what is going on in a device from a flow perspective.
>
> This view can be enabled by issuing the global configuration mode
> command **ip flow-top-talkers** and configuring the **top** command
> for the number of talkers (1--
>
> 200\) and the **sort-by** command to sort by bytes or packets,
> depending on the use case.
>
> Flexible NetFlow
>
> Flexible NetFlow was created to aid in more complex traffic analysis
> configuration than is possible with traditional NetFlow.
>
> Flexible NetFlow allows for the use and reuse of configuration
> components.
>
> Flexible NetFlow allows for the use of multiple flow monitors on the
> same traffic at the same time. This means that multiple different flow
> policies can be applied to the same traffic as it flows through a
> device.

Table 24-9 Flexible NetFlow Components

> Sampled NetFlow Data Trade-offs
>
> There are trade-offs in using sampled NetFlow data.
>
> The biggest one is that there is a reduced load on the device in terms
> of memory and CPU. However, by sampling NetFlow data only at specific
> intervals, something could be missed as the accuracy goes down with
> sampling compared to when gathering all data.
>
> Security has been a huge driver in the adoption of Flexible NetFlow
> due to its ability to track all parts of the IP header, as well as the
> packet and normalize it into flows.
>
> • Flexible NetFlow can dynamically create individual caches for each
> type of flow.
>
> • Flexible NetFlow can filter ingress traffic destined to a single
> destination.
>
> You can use the **collect** and **match** commands to create a
> customized flow record.
>
> To create a custom flow record, certain key and non-key fields must be
> matched so the flow record is usable. The **match** command is used to
> select key fields, and the **collect** command is used to select
> non-key fields.
>
> Table 24-10 shows a list of the key and non-key fields that can be
> used to mimic the original
>
> NetFlow capabilities when building a custom flow record.
>
> Table 24-10 Flow Record Key and Non-Key Fields

> Configuring flow records is an important step in enabling Flexible
> NetFlow. because the flow record defines what type of traffic will be
> analyzed or monitored.
>
> • There are predefined flow records, and you can also create custom
> flow records.
>
> • Custom flow records can have hundreds of different combinations to
> meet the exact needs of the business.
>
> Configuring a custom flow record involves the following steps:
>
> **1**. Define the flow record name.
>
> **2**. Set a useful description of the flow record.
>
> **3**. Set match criteria for key fields.
>
> **4**. Define non-key fields to be collected.

![](media/image26.png)

> Although many of the predefined flow records that are available may be
> suitable for many use cases, there are too many
>
> of them to cover here.
>
> Having the ability to build a custom flow record for a specific and
> unique use case makes it extremely powerful.
>
> Example 24-40 shows a custom flow record called CUSTOM1.
>
> Configuring the Custom Flow Exporter
>
> ![](media/image27.jpg)Now that a custom flow record has been
>
> configured, the flow exporter can be created.
>
> There are a few important steps to complete when building a flow
> exporter:
>
> 1\. Define the flow exporter name.
>
> 2\. Set a useful description of the flow exporter.
>
> 3\. Specify the destination of the flow exporter to be used.
>
> 4\. Specify NetFlow version to export.
>
> 5\. Specify the UDP port.
>
> Example 24-41 illustrates the configuration of the flow exporter as
> well as how to verify the configuration.
>
> Configure a Flow Monitor
>
> Now that a custom flow exporter has been configured, the flow monitor
> must be created.
>
> • Each flow monitor requires a flow record to be assigned to it.
>
> • Each flow monitor has its own cache, and the flow record provides
> the layout and how to carve up the cache for the defined traffic
> defined in the flow record.
>
> To configure a flow monitor, the following high-level steps must be
> taken:
>
> **1**. Define the flow monitor name.
>
> **2**. Set a useful description of the flow monitor.
>
> **3**. Specify the flow record to be used.
>
> **4**. Specify a cache timeout of 60 for active connections.
>
> **5**. Assign the exporter to the monitor.
>
> The cache timeout tells the device to export the cache to the
> collector every 60 seconds. It is important when creating a flow
> monitor for the description of the flow monitor to be useful and to
> map back to the flow record.
>
> Configuring the Custom Flow Monitor
>
> ![](media/image28.png)When configuring QoS, it is nice to have the
> descriptions self-document the intent of what the policy is doing.
>
> This helps when configuring the flow monitor and when using context
> sensitive help, as the description that is configured shows in the
> output.
>
> Example 24-42 shows this as well as the configuration and verification
> for the flow monitor called CUSTOM1.
>
> Configuring the Flow Exporter Mapping
>
> ![](media/image29.jpg)The next step is to map the flow exporter
>
> CUSTOM1 to the flow monitor CUSTOM1.
>
> You need to essentially map the two together so the traffic that is
> being collected by the flow record can be exported to the NetFlow
> collector at 192.168.14.100.
>
> Example 24-43 shows the process and verification for adding the flow
> exporter CUSTOM1 to the flow monitor CUSTOM1 on R4.
>
> Configuring the Flow Monitor Interface
>
> ![](media/image30.png)The final step necessary in enabling Flexible
> NetFlow is to apply the flow monitor to the interfaces.
>
> This step turns on the collection of NetFlow statistics, and it can be
> enabled for ingress or egress or both.
>
> Example 24-44 illustrates the process as well as how to verify that
> Flexible NetFlow is working by issuing the **show ip flow monitor
> CUSTOM1 cache** command.
>
> Switched Port Analyzer
>
> (SPAN) Technologies
>
> When the problem appears to be a Layer 2 issue, there are a few
> options:
>
> • Insert a splitter between the devices.
>
> • Configure the network device to mirror the packets.
>
> • Insert a switch between the two devices and then configure the
> switch to mirror the transient traffic to a traffic analyzer.
>
> Catalyst switches provide the Switched Port Analyzer (SPAN), which
> makes it possible to capture packets using the second two options
> above by using the following techniques:
>
> ![](media/image31.jpg)Figure 24-4 shows a sample topology with four
> computers (PC-A, PC-B, PC-C, and PC-D) spread across three switches
> and a traffic analyzer connected to SW1. PC-A, PC-B, and PC-C are all
> connected to VLAN 123 on the 10.123.1.0/24 network, and PC-D is
> connected to VLAN 34, which is on the 10.34.1.0/24 network. This
> topology is used to demonstrate the concepts of SPAN, RSPAN, and
> ERSPAN.
>
> A local SPAN session is the most basic form of packet capture as all
> the configuration occurs on a single switch. The destination of the
> mirrored traffic can be one or more local ports. The source of the
> packet capture can be only one of the following:
>
> • One or more specific switch ports
>
> • A port channel (also known as an EtherChannel)
>
> • A VLAN
>
> Also consider the following:
>
> • Most switches support at least two SPAN sessions, but newer hardware
> can support more
>
> than two sessions.
>
> • The source port cannot be reused between two different SPAN
> sessions.
>
> • Source ports can be switched or routed ports.
>
> • The destination cannot be reused between two different SPAN
> sessions.
>
> • It is possible to saturate the destination port if the source ports
> are receiving more data than
>
> the destination port can transmit.
>
> The source ports are defined with the global configuration command
> **monitor session** *session-id* **source** {**interface**
> *interface-id* \| **vlan** *vlan-id*} \[**rx** \| **tx** \|
> **both**\]. The SPAN *session- id* allows for the switch to correlate
> the source ports to specific destination ports.
>
> The direction of the traffic can be specified as part of the
> configuration. With the optional **rx** keyword you capture only
> traffic received on that source, with the optional **tx** key word you
> capture traffic sent by that source, and with the **both** keyword you
> capture all traffic.
>
> You can specify a trunk port as a source port to capture traffic for
> all VLANs that traverse that port. This might provide too much data
> and add noise to the traffic analysis tool. The VLANs can be filtered
> on the capture with the command **monitor session** *session-id*
> **filter vlan** *vlan-range*.
>
> The destination port is specified with the global configuration
> command:
>
> **monitor session** *session-id* **destination interface**
> *interface-id* \[**encapsulation**
>
> {**dot1q** \[**ingress** {**dot1q vlan** *vlan-id* \| **untagged
> vlan** *vlan-id* \| **vlan** *vlan-id*}
>
> \| **replicate** \[**ingress** {**dot1q vlan** *vlan-id* \| **untagged
> vlan** *vlan-id*\]}} \|
>
> **ingress**\]
>
> As you can see, there are a lot of different nested options.
>
> A SPAN session normally copies the packets without including any
> 802.1Q VLAN tags or Layer 2 protocols. Using the **encapsulation
> replicate** keywords includes that information. The full global
> configuration command is:
>
> **monitor session** *session-id* **destination interface**
> *interface-id* \[**encapsulation replicate**\]
>
> If the traffic analyzer is a Windows PC and is accessed using RDP, the
> port must be able to send and receive traffic for the Windows PC in
> addition to the traffic from the SPAN session. Situations like this
> require the following global configuration command:
>
> **monitor session** *session-id* **destination interface**
> *interface-id* **ingress** {**dot1q**
>
> **vlan** *vlan-id* \| **untagged vlan** *vlan-id*}
>
> Selecting the **dot1q** keyword requires the packets to be
> encapsulated with the specified VLAN ID. Selecting the **untagged**
> keyword accepts incoming packets and associates them to the specified
> VLAN ID.
>
> STP is disabled on the destination port to prevent extra BPDUs from
> being included in the network analysis. Great care should be taken to
> prevent a forwarding loop on this port.
>
> Example 24-45 shows how to monitor both PC-A's and PC-B's
> communication on SW1
>
> and send it toward the local traffic analyzer.
>
> ![](media/image32.png)
>
> A specific SPAN session can be viewed, or the output can be restricted
> to the local SPAN
>
> ![](media/image33.jpg)session, as shown in Example 24-46.
>
> ![](media/image34.png)The next example illustrates monitoring the
> trunk port Gi1/0/10 and provides the output to PC-B for PC-A and PC-B
> communication on SW1 and sending it toward the
>
> local traffic analyzer.
>
> Example 24-47 shows the commands that are entered on SW1 and then
> shows the configuration verified by examining the SPAN session.
>
> ![](media/image35.jpg)In the last scenario, the switch is configured
> to monitor PC-A's traffic, and it uses an already installed network
> traffic analysis tool on PC-B.
>
> When the switch is configured, PC- B can be accessed remotely to
>
> view the network traffic by using
>
> RDP.
>
> Example 24-48 lists the commands that are entered on SW1 to capture
> the ingress traffic and shows the configuration being verified.
>
> Remote SPAN (RSPAN)
>
> In large environments, it might be not be possible to move a network
> analyzer to other parts of the network. Example 24-49 shows the RSPAN
> VLAN being created on SW1 and SW2.
>
> ![](media/image36.png)
>
> Example 24-50 shows the configuration of RSPAN on the source switch,
> SW2. Traffic from
>
> PC-C is sent to SW1 for analysis.
>
> ![](media/image37.png)
>
> Configuration of RSPAN on the Destination Switch
>
> Example 24-51 shows the configuration of RSPAN on the destination
> switch, SW1. The traffic is sent to the traffic analyzer for analysis.
>
> ![](media/image38.png)
>
> Example 24-52 verifies the configuration of RSPAN on both SW1 and SW2.
>
> ![](media/image39.png)
>
> In large environments, it might not be possible to move a network
> analyzer to other parts of the network. ERSPAN provides the ability to
> monitor traffic in one area of the network and route the SPAN traffic
> to a traffic analyzer in another area of the network through Layer 3
> routing.
>
> **Specifying the Source Ports**
>
> A source and destination must be configured. To configure a source,
> the following command is issued: **monitor session**
> *span-session-number* **type erspan-source**. This defines the session
> number as well as the session type, **erspan-source**.
>
> Once the initial session is created, the source must be defined in the
> session. This is accomplished by issuing the **source** {
> **interface** *type number* \| **vlan** *vlan-ID* } \[ , \| - \|
> *both* \| *rx* \| *tx* \] command.
>
> When the source has been configured, it is necessary to configure the
> destination of the ERSPAN session. To enter the destination
> subconfiguration mode, the **destination** command is used. The rest
> of the commands will be issued in the destination subconfiguration
> mode to specify the destination of the ERSPAN session as well as any
> parameters associated with the configuration of the destination.
>
> The next step is to identify the IP address of the destination for the
> ERSPAN session. Because this is a Layer 3 SPAN session, this IP
> address is where the traffic will be sent to be analyzed. The command
> to configure this action is simply **ip address** *ip-address*.
>
> The final step is to assign a ToS or TTL to the ERSPAN traffic. This
> is done with the
>
> **erspan** { **tos** *tos-value* \| **ttl** t*tl-value* } command from
> global configuration mode.
>
> ![](media/image40.png)ERSPAN Process
>
> Example 24-53 illustrates this whole process. In addition, to verify
> the configured sessions, the **show monitor session erspan-source
> session** is issued on SW1.
>
> IP SLA
>
> IP SLA is a tool built into Cisco IOS software that allows for the
> continuous monitoring of
>
> various aspects of the network.
>
> ![](media/image42.jpg)Typically, any SLA received from a service
> provider only monitors or guarantees the traffic as it flows across
> the service provider's network. Figure 24-5 shows this scenario and
> illustrates why IP SLA provides more visibility that a typical service
> provider SLA.
>
> Although there are many different options and probes available for IP
> SLA, this section focuses only on the ICMP echo and HTTP operations of
> IP SLA. The ICMP echo operation can functionally be thought of as
> testing reachability by leveraging ICMP echo and echo replies or
> pings. Figure 24-6 illustrates how the ICMP echo operation works in IP
> SLA.
>
> ![](media/image43.jpg)
>
> To configure any IP SLA operation, the **ip sla** *operation-number*
> command must be used to enter IP SLA configuration mode, where
> *operation-number* is the configuration for the individual IP SLA
> probe. Once in IP SLA configuration mode, the command **icmp-echo**
> {*destination-ip-address* \| *destination-hostname*} \[**source-ip**
> {*ip-address* \| *hostname*} \| **source-interface**
> *interface-name*\] is used to configure the destination IP address of
> the device or host to be monitored.
>
> The next step is to specify how often the ICMP echo operation should
> run. This is accomplished by issuing the **frequency** *seconds*
> command. Example 24-54 shows the process covered so far on R1.
>
> ![](media/image44.png)

![](media/image45.jpg)

> When the IP SLA configuration is complete, an important step is to
> schedule and activate the IP SLA operation that has been configured.
> This is where the **ip sla schedule** *operation-number* \[**life**
> {**forever** \| *seconds*}\] \[**start-time** {\[*hh:mm:ss*\] \[*month
> day* \| *day month*\] \| **pending** \| **now** \| **after**
> *hh:mm:ss*}\] \[**ageout** *seconds*\] \[**recurring**\] command comes
> into play.
>
> When the IP SLA operation is scheduled, it can be verified with the
> **show ip sla configuration** command.
>
> Example 24-55 illustrates the configuration steps to schedule the IP
> SLA 1 operation with a start time of now and a lifetime of forever.
>
> Another very common use case for IP SLA is to monitor HTTP
> destinations for operation. This can be done by using the HTTP GET
> operation of IP SLA. In order to configure this type of monitor, the
> **ip sla** *operation-number* command must be used to enter IP SLA
> configuration mode.
>
> When the operation number is specified, the next step is to configure
> the HTTP GET probe by issuing the command **http** {**get** \|
> **raw**} *url*\[**name-server** *ip-address*\] \[**version** *version-
> number*\] \[**source-ip** {*ip-address* \| *hostname*}\]
> \[**source-port** *port-number*\] \[**cache** {**enable** \|
> **disable**}\] \[**proxy** *proxy-url*\].
>
> When the probe is configured, as with any other IP SLA operation, this
> operation needs to be scheduled by using the command **ip sla
> schedule** *operation-number* \[**life** {**forever** \| *seconds*}\]
> \[**start-time** {\[*hh:mm:ss*\] \[*month day* \| *day month*\] \|
> **pending** \| **now** \| **after** *hh:mm:ss*}\] \[**ageout**
> *seconds*\] \[**recurring**\].
>
> Cisco DNA Center
>
> Assurance
>
> • Security has become one the most important pieces of the network,
> and users expect a better experience.
>
> • Customers demand a simple way to manage Day 0--2 operations and
> require a scalable and simple approach to running the net-work.
>
> • Cisco DNA Center Assurance provides a tool for handling the most
> relevant customer requirements.
>
> Cisco DNA Center
>
> Typically, when an issue arises in the network, a helpdesk ticket is
> created. However, by the time the network operations team gets the
> ticket assigned, the issue is either resolved on its own or the
> information provided in the ticket to assist with troubleshooting the
> issue is stale or out of date.
>
> Cisco DNA Center Assurance has Network Time Travel. Network Time
> Travel acts as a digital video recorder (DVR) for the network. Network
> Time Travel records what is going on in the environment using
> streaming telemetry and can play back something that happened in the
> past.
>
> ![](media/image46.jpg)Figure 24-7 shows the main Cisco DNA Center
> page.
>
> Cisco DNA Assurance
>
> Cisco DNA Assurance is part of Cisco DNA Center.
>
> • Assurance takes 30+ years of Cisco Technical Assistance Center (TAC)
> experience and puts it into a tool that uses machine learning to
> diagnose issues within a network.
>
> • In addition to finding and diagnosing the issues, Assurance gives
> guided remediation steps to fix the
>
> issue. The Assurance tab is shown in Figure 24-8.
>
> ![](media/image47.jpg)
>
> ![](media/image48.jpg)Cisco DNA Center Client 360 View
>
> From this view, you can do many
>
> different things.
>
> • You can click the user's name to see
>
> details related to that specific user.
>
> • You can click each device to see specifics about that device in the
> Client 360 view.
>
> Figure 24-10 shows the entire Client 360 view for the user Grace
> Smith.
>
> Cisco DNA Center Search Results
>
> The amount of information that this screen provides is tremendous. The
> following pieces of
>
> information have been gathered automatically:
>
> • Device type
>
> • OS version
>
> • MAC address
>
> • IPv4 address
>
> • VLAN ID
>
> • Connectivity status
>
> • When the device was last seen on the network
>
> • What device it is connected to
>
> • Wireless SSID
>
> • Last known location
>
> The timeline in the Client 360 view shows issues. This is also a
> Network Time Travel capability. Since Assurance records the telemetry,
> it is possible to search back in time to see exactly what has affected
> the user.
>
> Path Trace
>
> Assurance has a tool called Path Trace. Path Trace is a visual
> traceroute and diagnostic tool that can be run periodically or
> continuously, with a specific refresh interval.
>
> **Figure 24-11** *Cisco DNA Center Assurance*
>
> ![](media/image49.jpg)*Client 360 Path Trace*

The path trace output shows a topology view of the traceroute, and in
this instance, Path Trace has also detected that there is an access
control list (ACL) blocking the traffic from Grace's iPad to John's PC
(see Figure

24-12).

**Figure 24-12** *Cisco DNA Center Assurance*

*Client 360 Path Trace Output*

> ![](media/image50.jpg)
>
> Path Trace ACL Information
>
> ![](media/image51.jpg)By hovering over the ACL entry, the following
> information can be seen:
>
> • The ACL's name
>
> • The interface the ACL is applied to
>
> • The direction (ingress or
>
> egress)
>
> • The ACL result (permit or deny) Figure 24-13 shows the access list
> information found in this example.
>
> ![](media/image52.jpg)By clicking on one of the issues listed under
> Grace's Client 360 view, such as
>
> the P1 Onboarding issue, a user can investigate the
>
> root cause of the issue.
>
> Figure 24-14 shows the issues that are impacting Grace.
>
> Client 360 Root Cause and Remediation Steps

,..

1 f\'\'-\"1\\. *j\\;vl\'*

1 l- - -

> 0 0 0 •

![](media/image53.jpg)Wiroloss client took a tong timo to connoct (SSIO:
OCorpSSIO, AP:AP-4800,Bend:2 4 GHz) - Excossn1e

> tlme due to Association fallures

v Issues (71

\-

D-r•-•c•-ce-\"•po_tl•c.•.:\....a,.o..\_.,\...,.\_\...\_.

> *-* .*.*.*.*\...*·*..*n*\...\....*-*.\_*-c*,..\_*-*,
>
> \'\'\"\'\'\.....\_\...\....\_.,\_0,\_\...\_\...
>
> \...\...\...\...\_\...\...\_..\_.,r\.....r,-\..... .-••
>
> -\_-\....,-.\_-,s,\_•( -
>
> \_\... ,..

\-- \_- .. ..

\...

,\...,.\_\...\...\_,

,.,\_

> u •
>
> \_,..
>
> P - :-:-:.-.==::\':.. -
>
> *\...\...\... \--ILICO\\h·*
>
> ,.. \....,.\_ \.... ·\"\"\'o-11!1100\'
>
> \"\"\'
>
> ![](media/image54.jpg)- ·
>
> ·\--
>
> ![](media/image55.jpg)

1 \_,.\_,

,\_ . . ,[, .]{.underline} \...,\...,.. . \...\.....,\...\.....\_ \.....
\_

> 2 Qlltoa\...\... \...\...,.. ..\_\....\--\"\"\"\' ,\....\_
>
> lo..n.\"-.·\...\...-·- ..- \...\...\--
>
> 4 \_,\_Nitl ta!JIIN \...,\...\_\.....,.IWIC\_..,,\....\_,
> ..IIIIIOC\_.,. .
>
> Figure 24-15 *Cisco DNA Center Assurance Client 360*
>
> *Roof Cause and Guided Remediation Steps*
>
> Prepare for the Exam

![](media/image56.jpg)

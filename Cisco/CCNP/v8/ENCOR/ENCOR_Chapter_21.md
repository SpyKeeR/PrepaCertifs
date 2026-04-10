![](media/image1.jpg)

> Chapter 21: Troubleshooting
>
> Wireless Connectivity
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 21 Content
>
> **This chapter covers the following content:**
>
> • **Troubleshooting Client Connectivity from the WLC -** This section
> discusses how to use a wireless LAN controller as a troubleshooting
> tool to diagnose problems with wireless clients.
>
> • **Troubleshooting Connectivity Problems at the AP -** This section
> discusses how to diagnose problems between a wireless LAN controller
> and an AP that might affect wireless client connectivity.
>
> Troubleshooting Client
>
> Connectivity from WLC
>
> • Most of your time managing and monitoring a wireless network will be
> spent in the
>
> wireless LAN controller GUI.
>
> • You can access a wealth of troubleshooting information from the
> controller, if you know
>
> the client's MAC address.
>
> When one or more network users report that they are having problems,
> your first course of action should be to gather more information, ask
> questions, and try to notice patterns or similarities in the answers
> you receive.
>
> • Information from the user such as, "I cannot connect" or "The Wi-Fi
> is down" might mean that the user's device cannot associate, cannot
> get an IP address, or cannot authenticate.
>
> • If you get reports from many people in the same area, perhaps an AP
> is misconfigured or malfunctioning.
>
> • Reports from many areas or from a single service set identifier
> (SSID) may indicate
>
> problems with a controller configuration.
>
> If you receive a report of only one wireless user having problems, it
> might not make sense to spend time troubleshooting a controller, where
> many users are supported. Instead, you should focus on that one user's
> client device and its interaction with an AP.
>
> Figure 21-1 illustrates the following conditions that must be met for
> a successful association:
>
> • The client is within RF range of an
>
> AP and asks to associate.
>
> • The client authenticates.
>
> • The client requests and receives an IP address.

![](media/image2.jpg)**Figure 21-1** *Conditions for a Successful
Wireless Association*

> Cisco WLCs have two main GUI presentations, one for monitoring and one
> for more advanced configuration and monitoring.
>
> When you open a browser to the WLC management address, you see the
> default screen that is shown in Figure
>
> 21-2.
>
> The default screen displays network
>
> summary dashboard information on
>
> the right portion and monitoring tools in the list on the left.

![](media/image3.jpg)

> **Figure 21-2** *The Initial Default WLC Display*
>
> If you know a specific wireless client's MAC address, you can enter it
> into the search bar at the top right of the screen.
>
> For example, in Figure 21-3,
>
> 78:4b:87:7b:af:96 is the target of the search. Because that MAC
> address is known to the controller, a match is shown with a client
> icon below the search bar.

![](media/image4.jpg)

> **Figure 21-3** *Searching for a Client in the WLC GUI*
>
> The resulting details about the client are displayed in the Client
> View screen, shown in Figure 21-4.
>
> From this output, you can see many details about the client device
> listed in the left portion of the screen, and you can see connectivity
> and application information displayed on the right.

![](media/image5.jpg)

> **Figure 21-4** *Client Search Results*
>
> Before a controller will permit a client to fully associate with a
> basic service set (BSS), the client must progress through a sequence
> of states. Each state refers to a policy that the client must meet
> before moving on to the next state:
>
> **1. Start -** Client activity has just begun.
>
> **2. Association -** The client has requested 802.11 authentication
> and association with an
>
> AP.
>
> **3. Authentication -** The client must pass a Layer 2 Pre-Shared Key
> (PSK) or 802.1x
>
> authentication policy.
>
> **4. DHCP -** The WLC is waiting to learn the client's IP address from
> a Dynamic Host
>
> Configuration Protocol (DHCP) server.
>
> **5. Online -** The client has passed Layer 2 and Layer 3 policies,
> successfully associated,
>
> and can pass traffic.
>
> Information such as the wireless client's username (if known),
> hostname, wireless MAC address, wireless connection uptime, and the
> SSID used can be viewed in the left portion of the Client View screen.
>
> In Figure 21-4, the username is not known because the client does not
> authenticate itself with a username.

![](media/image6.jpg)

> **Figure 21-4** *Client Search Results*
>
> In Figure 21-5 the AP is receiving the client's signal strength at −76
> dBm and the SNR at 18 dB (both rather low values), causing the current
> data rate to fall to 29
>
> Mbps. A quick look at the Connection
>
> Score value reveals a low 20%.
>
> It is safe to assume that the client has moved too far away from the
> AP where it is associated, causing the signal strength to become too
> low to support faster performance.

![](media/image7.jpg)

> **Figure 21-5** *WLC Information About a Poorly Performing Client*
>
> ![](media/image8.jpg)Clicking on the Connection Score value displays
> further details in a popup window, as shown in Figure 21-6.
>
> The 20% value is the result of the client's current data rate (29
> Mbps) divided by the lower of the AP or client maximum data rate (144
> Mbps).
>
> The Client Actual Rate and Connection Score values are indicators of
> current performance, and the other graphs show what is possible
>
> on the AP and the client. **Figure 21-6** *Displaying Detailed Client
> Performance Information*
>
> Checking the Client's Mobility State
>
> • The WLC Client Search information includes a handy end-to-end
> graphical representation
>
> of a client's wireless connection.
>
> • When you scroll down below the General and Connectivity sections,
> you see a topology
>
> diagram like the one shown in Figure 21-7.
>
> • The WLC's name, management IP address, and model are displayed.
> Following the connection toward the right, you can see the AP name, IP
> address, and model where the client is associated. Moving further to
> the right, you can see that the client is associated to the AP. The
> client device is displayed with identifying information such as the
> device name, device type, VLAN number, and IP address.
>
> ![](media/image9.jpg)
>
> **Figure 21-7** *Displaying the Client Mobility State*
>
> Checking the Client's Wireless Policies
>
> ![](media/image10.jpg)By scrolling further down in the Client Search
> information, you can verify information about network, QoS, security,
> and other policies that affect the client, as shown in Figure 21-8.
>
> You can quickly learn the client's IP address, VLAN number, QoS policy
> level used by the WLAN, security policy (WPA2), encryption cipher
> (CCMP AES), and authentication type (PSK with no EAP).
>
> **Figure 21-8** *Displaying the Wireless Policies Used by a Client*
>
> Testing a Wireless Client
>
> When you search for a specific client, the information displayed is of
> a static nature because it is obtained as a snapshot at the time of
> the search. The client search will need to be refreshed to get
> up-to-date data. You
>
> can also obtain dynamic data by testing a
>
> client in real time.
>
> By scrolling to the bottom of the client search information, you can
> see the Client Test section, which offers links to four client testing
> tools:
>
> • **Ping Test**: The WLC sends five ICMP
>
> echo packets to the client's IP address and measures the response
> time, as shown in Figure 21-9.

![](media/image11.jpg)

> **Figure 21-9** *Testing Ping Response*
>
> *Times Between the WLC and Client*
>
> **Connection:** The WLC debugs the client for up to three minutes and
> checks each policy step as the client attempts to join the wireless
> network.
>
> ![](media/image12.jpg)
>
> **Figure 21-10** *Performing a Connection*
>
> *Test on a Successful Wireless Client*

Figure 21-10 shows a client that has successfully joined, and Figure
21-11 shows a client that failed Layer 2 authentication with a
pre-shared key because its key did not match the key configured on the
WLC.

> ![](media/image13.jpg)
>
> **Figure 21-11** *Performing a Connection*
>
> *Test on a Failed Wireless Client*
>
> **Event Log:** The WLC collects and displays a log of events as the
> client attempts to join the wireless network, as shown in Figure
> 21-12.
>
> This information is very complex and detailed and is usually more
> suited for Cisco TAC engineers.

![](media/image14.jpg)

> **Figure 21-12** *Collecting an Event Log of a Client Join Attempt*
>
> **Packet Capture:** The WLC enables a wireless packet capture at the
> AP where the client attempts to join, as shown in Figure 21-13.
>
> The captured data is saved to a specified FTP server, where it can be
> downloaded and analyzed using a packet analysis tool like Wireshark or
> LiveAction Omnipeek.

![](media/image15.jpg)

> **Figure 21-13** *Performing a Packet Capture of a Wireless Client*
>
> Troubleshooting Connectivity
>
> at the AP
>
> • In cases where you get reports from multiple users who are all
> having problems in the
>
> same general area, you might need to focus your efforts on an AP.
>
> • The problem could be as simple as a defective radio, where no
> clients are receiving a signal. In that case, you might have to go
> onsite to confirm that the transmitter is not working correctly.
>
> The split-MAC architecture creates several different points where you
> can troubleshoot. Successfully operating the lightweight AP and
> providing a working BSS require the following:
>
> • The AP must have connectivity to its access layer switch.
>
> • The AP must have connectivity to its WLC, unless it is operating in
> FlexConnect mode.

![](media/image16.jpg)

> First, verify the connectivity between an AP
>
> and a controller.
>
> The easiest approach is to simply look for the AP in the list of live
> APs that have joined the controller. If you know which controller the
> AP should join, open a management session to it. Enter the AP's name
> in the search bar.
>
> If the search reveals a live AP that is joined to the controller,
> information is displayed in the Access Point View screen, as shown in
> Figure 21-14.

![](media/image17.jpg)

> In Figure 21-14 the AP is named T2412- ap4, has an IP address and a
> valid CDP entry that shows the switch name and port number where it is
> connected. The AP has a live Ethernet connection with a switch and has
> working Power over Ethernet (PoE).
>
> In the right portion of the Access Point View screen, you can verify
> parameters related to the AP's wireless performance and RF conditions.
>
> Another important indicator is the noise level on a channel. Ideally,
> the noise level should be as low as possible, usually around −90 or
>
> −100 dBm, so that 802.11 signals can be
>
> received intelligibly and accurately.
>
> Figure 21-15 lists the 5 GHz channel 161 as having a high noise level
> of −80 dBm--- something that is not normal or ideal.

![](media/image18.jpg)

> **Figure 21-15** *Performance Summary Information*
>
> The channel information also shows an index of air quality. This is a
> measure of how competing and interfering devices affect the airtime
> quality or performance on a channel, presented as a number from 0
> (worst) to 100 (best).
>
> The AP shows the air quality of channel 11 as 97, which is very good.
> However, channel 161 is 59, which is of concern.
>
> You can scroll further down in the Access Point View screen to see
> detailed information about the AP including a list of clients it is
> supporting, RF troubleshooting information, clean air assessments, and
> a tool to reboot the AP.

![](media/image19.jpg)

> **Figure 21-15** *Performance Summary Information*
>
> In Figure 21-16, the RF Troubleshoot tab has been selected to display
> interferer data for the channels in the 5
>
> GHz band.
>
> There are no interfering neighbor or rogue APs, but there is a clean
> air interferer in channel 161 - the channel that the AP is using.

![](media/image20.jpg)

> **Figure 21-16** *Displaying Information About RF Interferers*

![](media/image21.jpg)

> Select the Clean Air tab to see more details about the interfering
> devices that have been detected.
>
> In Figure 21-17, the Active Interferers table lists one continuous
> transmitter device with a severity level of 45, a duty cycle of 100%,
> and an RSSI value of −78 dBm.
>
> The severity level indicates how badly the interferer is affecting the
> channel. The duty cycle represents the percentage of time the device
> is actually transmitting.
>
> ![](media/image22.jpg)Displaying Information About Clean Air (Cont.)
>
> The two bar graphs represent the percentage of time the device is
> using the channel and the received signal strength level of the
> device.
>
> If users are complaining about problems when they are around this AP,
> you should focus your efforts on tracking down the continuously
> transmitting device.
>
> The best outcome is if the device can be disabled or moved to an
> unused channel. If not, you will likely have to reconfigure the AP to
> use a different channel to move away from the interference.
>
> Prepare for the Exam
>
> Prepare for the Exam
>
> Key Topics for Chapter 21

![](media/image23.jpg)

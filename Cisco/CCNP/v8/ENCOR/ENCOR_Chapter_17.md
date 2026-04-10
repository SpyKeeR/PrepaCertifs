![](media/image1.jpg)

> Chapter 17: Wireless Signals
>
> and Modulation
>
> Instructor Materials
>
> CCNP Enterprise: Core Networking
>
> Chapter 17 Content
>
> **This chapter covers the following content:**
>
> **Understanding Basic Wireless Theory -** This section covers the
> basic theory behind radiofrequency (RF) signals, as well as measuring
> and comparing the power of RF signals.
>
> **Carrying Data over a Wireless Signal -** This section provides an
> overview of basic methods and standards that are involved in carrying
> data
>
> wirelessly between devices and the network.
>
> Understanding Basic
>
> Wireless Theory
>
> • Wireless signals travel as electromagnetic waves through the air
> from sender to receiver.
>
> • Frequency is a fundamental property of the waves involved in a
> wireless link.
>
> Basic Wireless Concepts
>
> In RF wireless communications, the sender (a transmitter) sends an
> alternating current into a section of wire (an antenna), which sets up
> moving electric and magnetic fields that propagate out and away from
> the antenna as traveling waves.
>
> ![](media/image2.jpg)• The electric and magnetic fields travel along
> together and are always at right angles to each other, as shown in
> *Figure 17-3*. The signal
>
> must keep changing, or alternating, by cycling up and down, to keep
> the electric and magnetic fields cycling and pushing ever outward.
>
> • Electromagnetic waves do not travel strictly in a straight line.
> Instead, they travel by expanding in all directions away from the
> antenna.
>
> • In free space, the electromagnetic waves
>
> expand outward in all three dimensions.

**Figure 17-3** *Traveling Electric and Magnetic Waves*

> Basic Wireless Concepts (Cont.)
>
> ![](media/image3.jpg)The waves produced from a tiny point antenna
> expand outward in a spherical shape. The waves will eventually reach
> the receiver, in addition to many other locations in other directions.
>
> • Figure 17-4 shows a simple idealistic antenna that is a single
> point, which is connected at the end of a wire at the sender.
>
> • At the receiving end of a wireless link, the process is reversed. As
> the electromagnetic waves reach the receiver's antenna, they induce an
> electrical signal. If everything works right, the received signal will
> be a reasonable copy of the original transmitted signal.
>
> **Figure 17-4** *Wave Propagation with an Idealistic Antenna*
>
> The waves involved in a wireless link can be measured and described in
> several ways. One fundamental property is the frequency of the wave,
> or the number of times the signal makes one complete up and down cycle
> in 1 second.
>
> ![](media/image4.jpg)• A cycle can begin as the signal rises from the
> center line, falls through the center line, and rises again to meet
> the center line.
>
> • A hertz (Hz) is the most commonly used frequency unit and
> corresponds to the number of cycles per second.
>
> • In Figure 17-5, suppose that 1 second has elapsed, as shown. During
> that 1 second, the signal progressed through four complete cycles.
> Therefore, its frequency is
>
> 4 cycles/second, or 4 hertz.
>
> **Figure 17-5** *Cycles Within a Wave*
>
> Frequency can vary over a very wide range. As frequency increases by
> orders of magnitude, the numbers can become quite large. To keep
> things simple, the frequency unit name can be modified to denote an
> increasing number of zeros, as listed in Table 17-2.
>
> **Table 17-2** Frequency Unit Names

> Continuous Frequency Spectrum
>
> ![](media/image5.jpg)Figure 17-6 shows a simple representation of the
> continuous frequency spectrum ranging from 0
>
> Hz to 1022 (or 1 followed by 22 zeros) Hz. At the low end of the
> spectrum are frequencies that are too low to be heard by the human
> ear, followed by audible sounds. The highest range of frequencies
> contains light, followed by X, gamma, and cosmic rays.
>
> **Figure 17-6** *Continuous Frequency Spectrum*

The frequency range from around 3 kHz to 300

GHz is commonly called radio frequency (RF). It includes many different
types of radio communication, such as low-frequency radio, AM radio,
shortwave radio, television, FM radio, microwave, and radar.

> Frequency Bands for Wireless LANs
>
> One of the two main frequency ranges used for wireless LAN
> communication lies between
>
> 2.400 and 2.4835 GHz. This is usually called the 2.4 GHz band, even
> though it does not
>
> encompass the entire range between 2.4 and 2.5 GHz.
>
> The other wireless LAN range is usually called the 5 GHz band because
> it lies between 5.150 and 5.825 GHz. The 5 GHz band actually contains
> the following four separate and distinct bands:
>
> 5.150 to 5.250 GHz
>
> 5.250 to 5.350 GHz
>
> 5.470 to 5.725 GHz
>
> 5.725 to 5.825 GHz
>
> Most of the 5 GHz bands are contiguous except for a gap between 5.350
> and 5.470. At the
>
> time of this writing, this gap exists and cannot be used for wireless
> LANs.
>
> Understanding Frequency - Channels
>
> Frequency bands are usually divided up into a number of distinct
> channels. Each channel is known by a channel number and is assigned to
> a specific frequency. As long as the channels are defined by a
> national or international standards body, they can be used
> consistently in all locations.
>
> Figure 17-7 shows the channel assignment for the 2.4 GHz band that is
> used for wireless LAN communication. The band contains 14 channels
> numbered 1 through
>
> 14, each assigned a specific frequency.
>
> ![](media/image6.jpg)
>
> **Figure 17-7** *Example of Channel Spacing in the 2.4 GHz Band*
>
> The actual frequency range needed for the transmitted signal is known
> as the signal *bandwidth*, as shown in Figure 17-8. As its name
> implies, bandwidth refers to the width of frequency space required
> within the band.
>
> ![](media/image7.jpg)In wireless LANs, the signal bandwidth is defined
> as part of a standard. Even though the signal might extend farther
> above and below the center frequency than the bandwidth allows,
> wireless devices will use something called a spectral mask to ignore
> parts of the signal that fall outside the bandwidth boundaries.
>
> **Figure 17-8** *Signal Bandwidth*

© 2016 Cisco and/or its affiliates. All rights reserved. Cisco
Confidential 11

> Ideally, the signal bandwidth should be less than the channel width so
> that a different signal could be transmitted on every possible
> channel, with no chance that two signals could overlap and interfere
> with each other.
>
> ![](media/image8.jpg)When the signal bandwidth is wider than the
> channel assignment, the signals overlap each other, as shown in Figure
> 17-10. Because of this, signals on adjacent channels cannot possibly
> coexist without interfering with each other.
>
> Signals must be placed on more distant channels to prevent
> overlapping, thus limiting the number of usable channels in the band.
>
> **Figure 17-10** *Overlapp*© *i*2*n*01*g*6 C*C*isc*h*o *a*nd*n*/o*n*r
> it*e*s a*l*ff*S*ilia*p*tes*a*. A*c*ll *i*ri*n*gh*g*ts reserved. Cisco
> Confidential 12
>
> Understanding Phase
>
> ![](media/image9.jpg)RF signals are very dependent upon timing because
> they are always in motion.
>
> The phase of a signal is a measure of shift in time relative to the
> start of a cycle.
>
> When two identical signals are produced at exactly the same time,
> their cycles match up and they are said to be in phase with each
> other. If one signal is delayed from the other, the two signals are
> said to be out of phase.
>
> **Figure 17-11** *Signals In and Out of Phase*

Signals that are in phase tend to add together, whereas signals that are
180 degrees out of phase tend to cancel each other out.

> Measuring Wavelength
>
> Wavelength is a measure of the physical distance that a wave travels
> over one complete cycle. Wavelength is usually designated by the Greek
> symbol lambda (λ).
>
> Regardless of the frequency, RF waves travel at a constant speed. In a
> vacuum, radio waves travel at exactly the speed of light; in air, the
> velocity is slightly less than the speed of light.
>
> Wavelength decreases as the frequency increases. As the wave cycles
> get smaller, they cover less distance.

![](media/image10.jpg)

> **Figure 17-12** *Examples of Increasing Frequency and Decreasing
> Wavelength*
>
> **Use of the dB logarithmic functions:**
>
> • The strength of a wave can be measured as its amplitude, the top to
> bottom peak.
>
> • The strength of an RF signal is usually measured by its power, in
> watts (W).
>
> • When power is measured in watts (W) or milliwatts (mW), it is
> considered to be an absolute power measurement.
>
> • Because absolute power values can fall anywhere within a huge range,
> from a tiny decimal number to hundreds, thousands, or greater values,
> we use logarithmic functions to transform exponential ranges into
> linear ones.
>
> • The decibel (dB) is a handy function that uses logarithms to compare
> one absolute measurement to another. It was originally developed to
> compare sound intensity levels, but it applies directly to power
> levels, too.
>
> The following equation is used to calculate a dB value, where P1 and
> P2 are the
>
> absolute power levels of two sources:
>
> ![](media/image11.jpg)
>
> ![](media/image12.jpg)P2 represents the source of interest, and P1 is
> usually called the reference value or the source of comparison. The
> difference between the two logarithmic functions can be rewritten as a
> single logarithm of P2 divided by P1, as follows:
>
> The ratio of the two absolute power values is computed first; then the
> result is converted onto a logarithmic scale. The ratio or division
> form of the equation is the most commonly used in the wireless
> engineering world.
>
> **Important dB laws are as follows:**
>
> **Law of Zero:** A value of 0 dB means that the two absolute power
> values are equal. If the two power values are equal, the ratio inside
> the logarithm is 1, and the log10(1) is 0. This law is intuitive; if
> two power levels are the same, one is 0 dB greater than the other.
>
> **Law of 3s:** A value of 3 dB means that the power value of interest
> is double the reference value; a value of
>
> −3 dB means the power value of interest is half the reference. When P2
> is twice P1, the ratio is always 2. Therefore, 10log10(2) = 3 dB. When
> the ratio is 1/2, 10log10(1/2) = −3 dB.The Law of 3s is not very
> intuitive, but is still easy to learn. Whenever a power level doubles,
> it increases by 3 dB. Whenever it is cut in half, it decreases by 3
> dB.
>
> **Law of 10s:** A value of 10 dB means that the power value of
> interest is 10 times the reference value; a value
>
> of −10 dB means the power value of interest is 1/10 of the reference.
>
> •When P2 is 10 times P1, the ratio is always 10. Therefore,
> 10log10(10) = 10 dB.
>
> •When P2 is one tenth of P1, then the ratio is 1/10 and 10log10(1/10)
> = −10 dB.
>
> •The Law of 10s is intuitive because multiplying or dividing by 10
> adds or subtracts 10 dB, respectively.
>
> When absolute power values multiply, the dB value is positive and can
> be added. When the power values divide, the dB value is negative and
> can be subtracted. Table 17-3 summarizes the useful dB comparisons.
>
> **Table 17-3** Power Changes and Their Corresponding dB Values

> Sources D and E have power levels 5 and 200 mW. Try to figure out a
> way to go from 5 to 200 using only × 2 or × 10 operations.
>
> • Using the x2 and x10 operations, double 5 to get 10, then double 10
> to 20. Multiply by 10 to reach 200 mW. (E=D x 2 x 2 x 10)
>
> • Use the dB laws to replace the doubling and x10 with the dB
> equivalents. The result is E=D + 3 + 3 + 10 dB or E=D + 16 dB

![](media/image13.jpg)

> **Figure 17-17** *Example of Computing dB*
>
> *with Simple Rules*
>
> Understanding RF Power and dB
>
> Beyond comparing two transmitting sources, a network engineer must be
> concerned about the
>
> RF signal propagating from a transmitter to a receiver. The dB formula
> to compare the
>
> ![](media/image14.png)received signal strength to the transmitted
> signal strength is:
>
> The absolute power values at the transmitter and receiver can be
> converted to dBm, the results of which are shown in Figure 17-19.
> Notice that the dBm values can be added along the path: The
> transmitter dBm plus the net loss in dB equals the received signal in
> dBm.
>
> ![](media/image15.jpg)
>
> **Figure 17-19** *Subtracting dB to Represent a Loss in Signal
> Strength*
>
> Measuring Power Changes Along the Signal Path
>
> A transmitter, its antenna, and the cable that connects them are all
> discrete components that not only propagate an RF signal but also
> affect its absolute power level.
>
> • Transmitter power is usually a known value, expressed in mW.
>
> • When an antenna is connected to a transmitter, it provides some
> amount of gain to the resulting RF signal. An antenna's gain is
> measured by comparing its performance with that of a reference antenna
> (usually an *isotropic* antenna), then computing a value in dB.
>
> • An isotropic antenna does not actually exist because it is ideal in
> every way. The isotropic antenna's performance can be calculated
> according to RF formulas, making it a universal reference for any
> antenna.
>
> • Some signal loss occurs due to the physical qualities of the cable
> that connects an antenna to a transmitter, Cable vendors supply the
> loss values in dB per foot or meter of cable length for each type of
> cable manufactured.
>
> Measuring Power Changes Along the Signal Path (Cont.)
>
> The effective isotropic radiated power *(*EIRP*)* is the actual power
> level that will be radiated from the antenna. This value is calculated
> as a combination of transmitter power, the loss from the length of
> cable, and the antenna gain. The formula to calculate EIRP: EIRP = Tx
> Power -- Tx Cable + Tx Antenna. EIRP is regulated by government
> agencies in most countries, a signal cannot exceed the maximum
> allowable EIRP.
>
> A link budget is the power levels across the entire path from
> transmitter to receiver. To
>
> ![](media/image16.jpg)calculate the received signal strength, begin
> with the transmitter power expressed in dBm, add or subtract the dB
> components along the signal path to find the signal strength that
> arrives at the receiver.
>
> **Figure 17-22** *Example of Calculating Received Signal Strength*
>
> Free Space Path Loss • Whenever an RF signal is transmitted from an
> antenna, its amplitude decreases as it travels through
>
> free space.
>
> ![](media/image17.jpg)• Even if there are no obstacles in the path
> between the transmitter and receiver, the signal strength will weaken.
> This is known as free space path loss.
>
> • If the antenna is a point the RF data wave energy travels in every
> direction from the antenna. The wave that is produced takes the form
> of a sphere.
>
> • As energy is transmitted from the antenna, the sphere expands in
> free space.
>
> • Regardless of the antenna used, the amount of free
>
> space path loss through free space is consistent. Two
>
> **Figure 17-23** *Free Space Loss Due to Wave Spreading*

facts:

> • Free space path loss is an exponential function; the signal strength
> falls off quickly near the transmitter but more slowly farther away.
>
> • The loss is a function of distance and frequency

only.

© 2016 Cisco and/or its affiliates. All rights reserved. Cisco
Confidential 23

> Free Space Path Loss (Cont.)
>
> Free space path loss is greater in the 5 GHz band than it is in the
> 2.4 GHz band. In the equation, as the frequency increases, so does the
> loss in dB.
>
> Figure 17-24 shows the range difference, where both transmitters have
> an equal EIRP. The dashed circles show where the effective range ends,
> at the point where the signal strength of each transmitter is equal.

![](media/image18.jpg)

> **Figure 17-24** *Effective Range of 2.4 GHz and 5 GHz Transmitters*
>
> Power Levels at the Receiver
>
> Receivers usually measure a signal's power level according to the
> received signal strength
>
> indicator (RSSI) scale.
>
> ![](media/image19.jpg)The RSSI value is defined in the 802.11 standard
> as an internal 1-byte relative value ranging from 0 to 255, where 0 is
> the weakest and 255 is the strongest. The range of RSSI values can
> vary between one hardware manufacturer and another.
>
> Every receiver has a sensitivity level, or a threshold that divides
> intelligible, useful signals from unintelligible ones. As long as a
> signal is received with a power level that is greater than the
> sensitivity level, chances
>
> are that the data from the signal can be understood correctly.
>
> **Figure 17-25** *Example of Receiver Sensitivity Level*
>
> Power Levels at the Receiver (Cont.)
>
> The RSSI value focuses on the expected signal alone, without regard to
> any other signals that may also be received. All other signals that
> are received on the same frequency as the one you are trying to
> receive are simply viewed as noise. The noise level, or the average
> signal strength of the noise, is called the noise floor.
>
> The difference between the signal and the noise is called the
> signal-to-noise ratio (SNR), measured in dB. A higher SNR value is
> preferred.
>
> ![](media/image20.jpg)
>
> **Figure 17-26** *Example of a Changing Noise Floor and SNR*
>
> Carrying Data Over an RF
>
> Signal
>
> • Modulation is the process by which a carrier signal is changed in
> order to carry a data signal.
>
> • Modulation schemes can alter frequency, phase or amplitude of the
> signal to indicate
>
> the zeroes and ones within the data transmission.
>
> Modulation
>
> • To add data to the RF signal, the frequency of the original carrier
> signal must be preserved. Therefore, there must be some scheme of
> altering some characteristic of the carrier signal to distinguish a 0
> bit from a 1 bit.
>
> • Altering the carrier signal is known as modulation, where the
> carrier signal is modulated or changed according to some other source.
> At the receiver, the process is reversed; demodulation interprets the
> added information based on changes in the carrier signal.
>
> • RF modulation schemes generally have the following goals:
>
> • Be reasonably immune to interference and noise
>
> • Be practical to transmit and receive
>
> • Due to the physical properties of an RF signal, a modulation scheme
> can alter only the following attributes:
>
> • Frequency, but only by varying slightly above or below the carrier
> frequency
>
> • Phase
>
> • Amplitude
>
> Modulation (Cont.)
>
> • The modulation techniques require some amount of bandwidth centered
> on the carrier frequency due to the rate of the data being carried and
> partly due to the overhead from encoding the data and manipulating the
> carrier signal.
>
> • Narrowband transmissions, such as audio signals over an AM or FM
> radio, have a relatively low bit rate and little overhead.
>
> • Wireless LANs must carry data at high bit rates, requiring more
> bandwidth for modulation.
>
> Data being sent is spread out across a range of frequencies, known as
> spread spectrum. Two common spread-spectrum categories:
>
> **Direct sequence spread spectrum (DSSS):** Used in the 2.4 GHz band,
> where a small number of fixed, wide channels support complex phase
> modulation schemes and somewhat scalable data rates, making it more
> resilient to disruption.
>
> **Orthogonal Frequency Division Multiplexing (OFDM):** Used in both
> 2.4 and
>
> 5 GHz bands, where a single 20 MHz channel contains data that is sent
> in parallel over multiple frequencies. Each channel is divided into
> many subcarriers (also called subchannels or tones); both phase and
> amplitude are modulated with quadrature amplitude modulation (QAM) to
> move the most data efficiently.
>
> Each step in the 802.11 evolution involves an amendment to the
> standard, defining things like modulation and coding schemes that are
> used to carry data over the air.
>
> A summary of common amendments to the 802.11 standard, along with the
> permitted bands,
>
> supported data rates, and channel width, is shown in Table17-4.
>
> **Table 17-4** A Summary of Common 802.11 Standard Amendments
>
> 54 Mbps
>
> 54 Mbps
>
> spatial streams
>
> spatial streams spatial streams
>
> \*802.11ax is designed to work on any band from 1 to 7 GHz, provided
> that the band is approved for use.
>
> Newer Wi-Fi Standards include the following:
>
> • The 802.11n amendment was published in 2009 in an effort to scale
> wireless LAN performance to a theoretical maximum of 600 Mbps. The
> amendment was unique because it defined a number of additional
> techniques known as high throughput (HT) that can be applied to either
> the 2.4 or 5 GHz band.
>
> • The 802.11ac amendment was introduced in 2013 and brought even
> higher data rates through more advanced modulation and coding schemes,
> wider channel widths, greater data aggregation during a transmission,
> and so on. 802.11ac is known as very high throughput (VHT) wireless
> and can be used only on the 5 GHz band.
>
> • The 802.11ax amendment, also known as Wi-Fi 6 and high efficiency
> wireless, aims to change the principle that only one device can claim
> airtime at a time by permitting multiple devices to transmit during
> the same window of air time. This becomes important in areas that have
> a high density of wireless devices, all competing for air time and
> throughput. 802.11ax uses OFDM Access (OFDMA) to schedule and control
> access to the wireless medium, with channel air time allocated as
> resource units that can be used by multiple devices simultaneously.
>
> Using Multiple Radios to Scale Performance
>
> Before 802.11n, wireless devices used a single transmitter and a
> single receiver. In other words, the components formed one radio,
> resulting in a single radio chain. This is also known as a single-in,
> single-out (SISO) system.
>
> One secret to the better performance of 802.11n, 802.11ac, and
> 802.11ax is the use of multiple radio components, forming multiple
> radio chains. This is known as a multiple-input, multiple- output
> (MIMO) system.
>
> ![](media/image21.jpg)
>
> **Figure 17-28** *Examples of SISO and MIMO Devices*
>
> Spatial Multiplexing
>
> ![](media/image22.jpg)• To increase data throughput, data can be
> multiplexed or distributed across two or more radio chains---all
> operating on the same channel, but separated through spatial
> diversity. This is known as spatial multiplexing.
>
> • Spatial multiplexing requires a good deal of digital signal
> processing on both the transmitting and receiving ends. This pays off
> by increasing the throughput over the channel; the more
>
> spatial streams that are available, the more data
>
> that can be sent over the channel.
>
> • When the sender and receiver have mismatched spatial stream support,
> they negotiate the wireless connection and use the lowest number of
> special streams that they have in common.
>
> **Figure 17-29** *Spatial Multiplexing Between Two 3×3:2 MIMO Devices*
>
> ![](media/image23.jpg)Transmit Beamforming
>
> The 802.11n, 802.11ac, and 802.11ax amendments offer a method to
> customize the transmitted signal to prefer one receiver over others.
> By leveraging MIMO, the same signal can be transmitted over multiple
> antennas to reach specific client locations more efficiently.
>
> With *transmit beamforming (T*×*BF)*, the phase of the signal is
> altered as it is fed into each
>
> transmitting antenna so that the resulting signals will all arrive in
> phase at a specific receiver. Figure 17-30 shows a device on the left
> using transmit beamforming to target device B on the right.
>
> **Figure 17-30** *Using Transmit Beamforming to Target a Specific
> Receiving Device*
>
> When an RF signal is received on a device, it may be degraded or
> distorted due to a variety of conditions. If that same signal was
> transmitted over multiple antennas, as in the case of a MIMO device,
> then the receiving device can attempt to restore it to its original
> state.
>
> The receiving device can use multiple antennas and radio chains to
> receive the multiple transmitted copies of the signal. One copy might
> be better than the others, or one copy might be better for a time, and
> then become worse than the others. Maximal-ratio combining (MRC) can
> combine the copies to produce one signal that represents the best
> version at any given time.
>
> Dynamic Rate Shifting
>
> Figure 17-31 illustrates dynamic rate shifting
>
> (DRS) operation on the 2.4 GHz band.
>
> Each concentric circle represents the range supported by a particular
> modulation and coding scheme. Notice that the white circles denote
> OFDM modulation (802.11g), and the shaded circles contain DSSS
> modulation (802.11b).
>
> Each move of the receiver away from the transmitter, into a larger
> concentric circle, causes a dynamic shift to a reduced data rate, in
> an effort to maintain the data integrity to the outer reaches of the
> transmitter's range.

![](media/image24.jpg)

> **Figure 17-31** *Dynamic Rate Shifting as a Function of Range*
>
> Prepare for the Exam

![](media/image25.jpg)

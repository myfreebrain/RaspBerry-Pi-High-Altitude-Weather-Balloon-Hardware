# Raspberry Pi powered High Altitude Weather Balloon:

**The hardware of the weather balloon or the payload section is structured as a six layered stack of Raspberry Pi hats.**

---

<img align="right" width="500" src="https://github.com/MonkHelios/RaspBerry-Pi-High-Altitude-Weather-Balloon-Hardware/blob/master/Payload/Pictures/InkedLRM_EXPORT_825743803905478_20190919_195242457_LI.jpg">

- [x] The first layer is a _**Raspberry Pi**_ which manages operation of all other stacks and undertakes necessary processing tasks.
- [x] To power the entire stack we have a high current DC-DC converter as a _**power delivery unit**_ which accepts 1S LiPo or LiIon batteries as input and outputs a steady 5V and allows a maximum current draw of 7A.
- [x] For telemetry and other communication purposes we are using a _**CC1125 based RF board**_.
- [x] The next stack comprises of a _**GSM board**_ for non LOS communication at lower altitudes and a _**GPS board**_ for tracking the balloon and for easy retrieval. Since both of these are using the same serial channel of the Raspberry Pi, multiplexing and demultiplexing were necessary. This was facilitated by a _**Mux Demux board**_ which had the ability to select one peripheral among the two.
- [ ] Finally on top of the GPS hat we have the _**sensor hat**_.

---

## 1. Power Delivery Board:

To run the essential hardware stacks a power delivery system more capable than a Raspberry Pi's internal power distribution was required. A design of a power distribution stack which could supply a high enough current with stability was adopted. The board was powered with a 3.7V LiIon or LiPo cell, its output was a constant 5V with a maximum allowed current of 7A. Our required peak current was 5A so, a 2A headroom was kept. The design was built around the _**LTC1871-1**_ - a wide input range, current mode, boost, flyback or SEPIC controller that drives an N-channel power MOSFET and requires very few external components.

### 1.1 Schematic:

<p align="center">
  <img width="800" src="https://github.com/MonkHelios/RaspBerry-Pi-High-Altitude-Weather-Balloon-Hardware/blob/master/Payload/Hardware/Power_(Pi_Po)/Schematics%2BDesigns/schematic.png">
</p>

### 1.2 Composite:

<p align="center">
  <img width="800" src="https://github.com/MonkHelios/RaspBerry-Pi-High-Altitude-Weather-Balloon-Hardware/blob/master/Payload/Hardware/Power_(Pi_Po)/Schematics%2BDesigns/composite.png">
</p>

### 1.3 Assembly:

<img align="left" width="400" src="https://github.com/MonkHelios/RaspBerry-Pi-High-Altitude-Weather-Balloon-Hardware/blob/master/Payload/Hardware/Power_(Pi_Po)/Schematics%2BDesigns/assembly.png">

>**Comments on Revision 1.0 -** Assistance regarding _PCB layout, component placing & the schematic design_ was taken. Output voltage was as expected, as well as the ability to supply high currents. However, on probing the output with and oscilloscope it was found that the output waveform was quite noisy and had significant switching noise at the frequency of the used DC-DC converter. 
It was concluded that the PCB layout and component placement were the culprits for induction of switching noise _(To be addressed in rev 2.0)_. Hence, I would not recommend following the component placement and PCB layout guides present in _**LTC1871-1's**_ datasheet. Instead, Understand the guidelines given and apply common mutual induction principles while designing the output section. 

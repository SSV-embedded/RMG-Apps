# App CAN2UDP

The CAN-to-UDP forwarding is a bridge between the CAN bus and the User Datagram Protocol (UDP) in IP-based networks. It converts CAN frames to and from generic frames (as specified by CiA 315) and transmits these over UDP.  

# Info
- Software: https://opensource.lely.com/canopen/docs/can2udp/

# Example
## CAN-over-IP Bridge
The can2udp app can be used to connect two or more CAN networks over Ethernet or a mobile network.

![rmg941c_schema_can2ip_en](https://user-images.githubusercontent.com/85748650/122211599-3476e700-cea7-11eb-88d1-5878700c2f29.png)

To create a CAN-over-IP bridge two RMG/941C's are necessary, on which the can2udp app must be installed in each case.

# Usage
- App configuration: *SSV/WebUI* > *Services* > *CAN to UDP*.

![rmg941c_webui_can2udp](https://user-images.githubusercontent.com/85748650/122250012-99dbcf80-cec9-11eb-90c9-18190093ebc4.PNG)

This page allows to set the local UDP port as well as the remote IP address and UDP port.

**Please note: The IP addresses as well as the UDP ports on both RMG/941C's must be different!**

To set the CAN bitrate and to enable/disable the CAN termination resistor go to *SSV/WebUI* > *Network* > *CAN*.

![rmg941c_webui_can-interface](https://user-images.githubusercontent.com/85748650/122253038-1bccf800-cecc-11eb-8ff1-5b0badc3b715.PNG)

# App CAN2UDP

The CAN-to-UDP forwarding is a bridge between the CAN bus and the User Datagram Protocol (UDP) in IP-based networks. It converts CAN frames to and from generic frames (as specified by CiA 315) and transmits these over UDP.  

# Info
- The can2udp app is compatible with following SSV devices:
  - RMG/941C
  - RMG/941CL
  - RMG/941CN
- This Software was used to build the can2udp app: https://opensource.lely.com/canopen/docs/can2udp/

# Example
## CAN-over-IP Bridge
The can2udp app can be used to connect two or more CAN networks over Ethernet or a mobile network.

![rmg941c_schema_can2ip_1012px](https://user-images.githubusercontent.com/85748650/122586333-d429a600-d05c-11eb-86d8-7dc064e1ab5f.png)

To create a CAN-over-IP bridge two RMG/941C's are necessary, on which the can2udp app must be installed in each case.

# Usage

- CAN configuration: *SSV/WebUI* > *Network* > *CAN*.

Here you can enable the CAN interface, set the CAN bitrate and enable/disable the CAN termination resistor.

![rmg941c_webui_can-interface](https://user-images.githubusercontent.com/85748650/122253038-1bccf800-cecc-11eb-8ff1-5b0badc3b715.PNG)

- App configuration: *SSV/WebUI* > *Services* > *CAN to UDP*.

This page allows to set the local UDP port as well as the remote IP address and UDP port.

**Please note: The IP addresses as well as the UDP ports on both RMG/941C's must be different!**

![rmg941c_webui_can2udp](https://user-images.githubusercontent.com/85748650/122250012-99dbcf80-cec9-11eb-90c9-18190093ebc4.PNG)

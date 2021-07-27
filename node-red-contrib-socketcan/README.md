# App Node-RED Contrib SocketCAN
Node-RED nodes to read CAN frames from and send CAN frames to a CAN bus using SocketCAN.

# Info
- The node-red-contrib-socketcan app is compatible with following SSV devices:
  - RMG/941C(L, N)
- This app installs two nodes: a **CAN input node** (socketcan-out) as well as a **CAN output node** (socketcan-in). For more information please visit: **https://flows.nodered.org/node/node-red-contrib-socketcan**
- The CAN input node (socketcan-out) converts the received CAN data into a **JSON object** with a Unix timestamp like shown in the example below. 

# Example
![flow_socketcan](https://user-images.githubusercontent.com/85748650/127144160-9c6078a1-6b09-4bbe-83f1-cd4cd7df26eb.PNG)

Example of a JSON object with CAN data:
```
{
  "timestamp": 1623682765400,
  "ext": false,
  "canid": 1,
  "dlc": 8,
  "rtr": false,
  "data": [67, 65, 78, 49, 50, 53, 107, 98]
}
```
## CAN-to-Modbus Converter
**Please note: For this example the app [node-red-modbus2](https://github.com/SSV-embedded/RMG-Apps/tree/master/node-red-modbus2) must be installed on the RMG/941C.**

If the CAN input node (socketcan-out) resp. CAN output node (socketcan-in) is used with another protocol node, you can create a "CAN-to-X" protocol converter. The following figure shows an example of a CAN-to-Modbus converter:

![flow_can2modbus](https://user-images.githubusercontent.com/85748650/127149926-6c49ecfb-82c9-47db-8dbe-256011f627bc.png)

The *SocketCAN input node* (socketcan-out in the figure) creates a JSON object with CAN data. The *function node CAN2NUMBER* extracts the desired part from the JSON object which should be sent via Modbus-TCP. The actual Modbus-TCP interface to access the CAN data is the *Modbus TCP server node* on the right side.

This is the JavaScript code for the **CAN2NUMBER function node**:
```
/* Monitoring CAN-ID 256 (0x100) */
if (msg.payload.canid !== 256) {
    return;
}
/* Length 2 bytes */
if (msg.payload.dlc !== 2) {
    return;
}
/* no RTR messages */
if (msg.payload.rtr !== false) {
    return;
}

/* using big-endian byte order */
let val_h = msg.payload.data[0];
let val_l = msg.payload.data[1];

/* calculate the payload */
msg.payload = val_l + 256 * val_h;

return msg;
```
# Usage
1. Open *SSV/WebUI > System > Apps management* and install these apps on the RMG/941C:
    - node-red
    - node-red-contrib-socketcan

2. Open *SSV/WebUI > Network > CAN* to configure the CAN interface.
   
   Here you can enable the CAN interface, set the CAN bitrate and enable/disable the CAN termination resistor.

![rmg941c_webui_can-interface](https://user-images.githubusercontent.com/85748650/122253038-1bccf800-cecc-11eb-8ff1-5b0badc3b715.PNG)

3. Open *SSV/WebUI > Apps > Node-RED* and start Node-RED.
4. Open the Node-RED user interface and start to build your own flow with the SocketCAN nodes.

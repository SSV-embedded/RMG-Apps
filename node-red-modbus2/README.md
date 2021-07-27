# App Node-RED Modbus2
Node-RED nodes to communicate with Modbus devices via TCP/IP and RTU.

# Info
- The node-red-modbus2 app is compatible with following SSV devices:
  - RMG/941(L,N): TCP/IP and RTU
  - RMG/941C(L, N): TCP/IP only
- This app installs two nodes: a **Modbus master/client node** as well as a **Modbus slave/server node**.

# Example
![sample_modbus_flow](https://user-images.githubusercontent.com/85748650/127166303-0e9b31d8-e10b-4fe6-a754-8ab9216d37df.png)

This example shows one Modbus TCP client node which receives data from two inject nodes and sends it to a Modbus register and another Modbus TCP client node which polls data from a Modbus register and sends it to a debug node.

## CAN-to-Modbus Converter
**Please note: For this example the app [node-red-contrib_socketcan](https://github.com/SSV-embedded/RMG-Apps/tree/master/node-red-contrib-socketcan) must be installed on the RMG/941C.**

If a Modbus TCP server node is used with another protocol node, you can create an "X-to-Modbus" protocol converter. The following figure shows an example of a CAN-to-Modbus converter:

![flow_can2modbus](https://user-images.githubusercontent.com/85748650/127149926-6c49ecfb-82c9-47db-8dbe-256011f627bc.png)

The *SocketCAN input node* (socketcan-out in the figure) creates a JSON object with CAN data. The *function node CAN2NUMBER* extracts the desired part from the JSON object which should be sent via Modbus-TCP. The actual Modbus-TCP interface to access the CAN data is the *Modbus server node* on the right side.

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
1. Open *SSV/WebUI > System > Apps management* and install these apps on the RMG/941:
    - node-red
    - node-red-modbus2
2. Open *SSV/WebUI > Apps > Node-RED* and start Node-RED.
3. Open the Node-RED user interface and start to build your own flow with the Modbus nodes.

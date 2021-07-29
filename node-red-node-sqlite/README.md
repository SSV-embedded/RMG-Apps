# App Node-RED SQLite Database
Node-RED node to read and write a local SQLite database.

# Info
- The node-red-node-sqlite app is compatible with following SSV devices:
  - RMG/941(L,N)
  - RMG/941C(L, N)
- https://github.com/node-red/node-red-nodes/tree/master/storage/sqlite

# Example
The following example shows one *SQLite DB node* (test) which receives a timestamp as data over an inject node and writes it to an SQLite DB on the RMG/941. There are also nodes to create, load and drop a table as well as two debug nodes.
![sqlite_sample_flow](https://user-images.githubusercontent.com/85748650/127479380-a6400127-f5d3-481c-9c0b-7ea81e642698.png)

# Usage
1. Open *SSV/WebUI > System > Apps management* and install these apps on the RMG/941:
    - node-red
    - node-red-node-sqlite
2. Open *SSV/WebUI > Apps > Node-RED* and start Node-RED.
3. Open the Node-RED user interface and start to build your own flow with the SQLite node or import the SQLite sample flow.

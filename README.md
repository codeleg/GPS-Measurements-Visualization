Development of an Application for GPS Measurements Visualization

WebSocket Connection and Data Reading:

The code connects to a server at localhost:4001 using WebSocket.
It receives JSON formatted data from the server (via the onmessage event handler).
Based on the received data, if the data id is 'object', it updates the object's position using the updateObjectPosition function; otherwise, it updates the satellites' positions using the updateSatellitePosition function.
Graph Visualization:

A graph is created using the Plotly.js library (Plotly.newPlot).
Two different traces are defined: one representing satellites (Satellites) and the other representing the object (Object).
The updateObjectPosition and updateSatellitePosition functions update the graph traces based on the incoming data (using Plotly.restyle and Plotly.extendTraces).
API Configuration Update:

The user interface contains input fields (messageFrequency, satelliteSpeed, objectSpeed) for configuration data.
This data is sent as a POST request to localhost:4001/config using the fetch function.
The response from the server (response.json()) is logged to the console.
User Interface:

It offers a simple and clear user interface.
The layout includes a graph area (#plot), input fields, and an update button (Update Config).
The input fields have predefined initial values and limits (min, max).

Development of an Application for GPS Measurements Visualization

Project Overview
This project implements a web application that visualizes the positions of an object and satellites based on GPS measurements. The data is provided by an emulated GPS measurement service running in a Docker container. The application connects to the GPS emulator via WebSocket, processes the received data, and displays it on a Cartesian coordinate graph in real-time. Additionally, users can modify GPS parameters (such as message frequency, satellite speed, and object speed) through a simple API.

Features
WebSocket Data Connection: The application establishes a WebSocket connection to receive real-time data about the object and satellite positions.
Real-Time Data Visualization: The positions of the object and satellites are dynamically displayed on a graph in Cartesian coordinates using the Plotly.js library.
GPS Parameters Update via API: Users can update GPS settings like message frequency, satellite speed, and object speed using the API provided by the GPS emulator.
Intuitive User Interface: A simple and clean user interface enables users to visualize the positions and modify parameters without difficulty.
Project Workflow
WebSocket Connection: The application connects to the GPS emulator running at localhost:4001. It receives data from the emulator in JSON format. Each message contains information about the coordinates of satellites and the object.

Data Processing: The application processes the incoming data, differentiating between satellite positions and the object's position based on the id field. The satellite positions are represented by UUIDs, and the object's position is identified separately.

Graph Visualization:

The object and satellites' positions are plotted on a 2D Cartesian graph.
The Plotly.js library is used for graphical rendering, with different colors and markers representing the object and the satellites.
The graph updates in real-time as new data arrives via WebSocket.
Updating GPS Configuration:

Users can modify the GPS parameters (such as message frequency, satellite speed, and object speed) through an API using a POST request.
The application sends the updated parameters to the GPS emulator, and the system reflects the changes in real-time.
Instructions
1. Setting Up the GPS Emulator
To simulate the GPS measurements, you need to run the provided GPS emulator Docker image. Follow these steps:

Download the Docker image:

bash:

docker pull iperekrestov/university:gps-emulation-service
Run the GPS emulator:

bash :

docker run --name gps-emulator -p 4001:4000 iperekrestov/university:gps-emulation-service
This command will start the emulator, making it available at localhost:4001.

2. Running the Application
Clone the repository and install necessary dependencies.
Open the index.html file in a browser to launch the application.
The application will automatically establish a WebSocket connection to localhost:4001 and start receiving and visualizing the data.
3. Changing GPS Parameters
To change the configuration of the GPS measurements (such as message frequency, satellite speed, and object speed), you can use the following curl command:

bash :

curl -X POST http://localhost:4001/config -H "Content-Type: application/json" -d '{ "messageFrequency": 2, "satelliteSpeed": 120, "objectSpeed": 20 }'
Alternatively, the application interface includes input fields and an "Update Config" button, allowing users to modify these parameters directly from the web interface.

Key Technologies Used
WebSocket: For real-time communication with the GPS emulator.
Plotly.js: For visualizing the position of the object and satellites on a 2D graph.
HTML/CSS/JavaScript: To create the user interface and handle WebSocket data processing.
Docker: To run the GPS measurement emulator.
Structure of Incoming Data
The GPS emulator sends the following data via WebSocket:

json :

{
  "id": "uuid",
  "x": 100.5,
  "y": 200.3,
  "sentAt": 1692170400000,
  "receivedAt": 1692170400100
}
id: Unique identifier of the satellite (or object).
x, y: Cartesian coordinates of the satellite or object.
sentAt: Timestamp when the message was sent by the satellite (in milliseconds since Unix epoch).
receivedAt: Timestamp when the message was received by the object (in milliseconds since Unix epoch).

Conclusion

1-The code connects to a server at localhost:4001 using WebSocket.

It receives JSON formatted data from the server (via the onmessage event handler).
Based on the received data, if the data id is 'object', it updates the object's position using the updateObjectPosition function; otherwise, it updates the satellites' positions using the updateSatellitePosition function.

Graph Visualization:

2-A graph is created using the Plotly.js library (Plotly.newPlot).

Two different traces are defined: one representing satellites (Satellites) and the other representing the object (Object).
The updateObjectPosition and updateSatellitePosition functions update the graph traces based on the incoming data (using Plotly.restyle and Plotly.extendTraces).

API Configuration Update:

3-The user interface contains input fields (messageFrequency, satelliteSpeed, objectSpeed) for configuration data.

This data is sent as a POST request to localhost:4001/config using the fetch function.
The response from the server (response.json()) is logged to the console.

User Interface:

4-It offers a simple and clear user interface.

The layout includes a graph area (#plot), input fields, and an update button (Update Config).
The input fields have predefined initial values and limits (min, max).

Finally : 

This project successfully demonstrates a system for visualizing GPS measurements in real-time. The web application connects to an emulated GPS service, processes incoming data, and displays object and satellite positions graphically. Additionally, users can modify GPS settings dynamically, showcasing a practical application of WebSocket communication and data visualization in real-world scenarios like navigation systems.
WebSocket Connection and Data Reading

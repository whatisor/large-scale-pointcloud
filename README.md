# Large Scale Pointcloud Project

## Introduction
This project aims to provide a comprehensive solution for generating and visualizing large scale point clouds from image or video streams. The solution is designed to work with streams from phone cameras, which are sent to a server (either local or cloud-based). The server processes these streams to generate sparse point clouds, which are then converted into splats for visualization. The final output can be viewed in a web-based viewer.

## Principle Design
The design of this project is based on a three-step process:

1. **Image or Video Streaming**: The user streams images or videos from their phone camera to the server. This can be done either through image-based streaming or through WebRTC video and data channels for point cloud streaming.

2. **Sparse Point Cloud Generation**: The server receives the streams and processes them to generate sparse point clouds. This is done using the [open-sfm](https://github.com/whatisor/open-sfm) repository.

3. **Splat Generation and Visualization**: The sparse point clouds are then converted into splats using the [gaussian-splatting-cuda](https://github.com/whatisor/gaussian-splatting-cuda) repository. The splats can be visualized using the [gaussian-splats-3d](https://github.com/whatisor/gaussian-splat-3D) web-based viewer.

## Project Structure
This project is structured around three main repositories:

1. [gaussian-splatting-cuda](https://github.com/whatisor/gaussian-splatting-cuda): This repository is responsible for generating splats from images and point clouds.

2. [open-sfm](https://github.com/whatisor/OpenSfM): This repository is used to generate sparse point clouds, which serve as the base input for the gaussian-splatting-cuda repository.

3. [gaussian-splats-3d](https://github.com/whatisor/GaussianSplats3D): This is a web-based viewer for visualizing the output of the gaussian-splatting-cuda repository.

Each repository plays a crucial role in the overall functioning of the project, and they work together to provide a seamless experience for generating and visualizing large scale point clouds.

## 1st Approach: High-Level Design of Servers

To achieve the goal of generating and visualizing large scale point clouds, the project utilizes a server-based architecture. Here is a high-level design of the servers involved:

1. **Image/Video Streaming Server**: This server is responsible for receiving image or video streams from the user's phone camera. It can be implemented using technologies such as Node.js or Python with frameworks like Express or Flask. The server should provide endpoints for the user to send the streams and handle the incoming data.

2. **Processing Server**: Once the image or video streams are received, they are forwarded to the processing server. This server is responsible for processing the streams and generating sparse point clouds. The processing can be done using the open-sfm repository mentioned earlier. The server should have the necessary dependencies installed and configured to run the open-sfm algorithms.

3. **Splat Generation Server**: After the sparse point clouds are generated, they are sent to the splat generation server. This server utilizes the gaussian-splatting-cuda repository to convert the point clouds into splats. The server should have the required GPU resources and the gaussian-splatting-cuda library properly installed.

4. **Web-Based Viewer Server**: Finally, the splats are ready to be visualized. The web-based viewer server serves as the platform for visualizing the splats generated by the previous server. It hosts the gaussian-splats-3d repository, which provides a user-friendly interface for exploring and interacting with the point cloud data. The server should have the necessary web server software (e.g., Apache or Nginx) and the gaussian-splats-3d repository properly deployed.

By dividing the functionality into separate servers, the project achieves modularity and scalability. Each server can be deployed and scaled independently, allowing for efficient resource utilization and easy maintenance.

## 1st Approach: Server Communication using gRPC

To enhance the communication between the servers in the large scale point cloud project, we can utilize gRPC, a high-performance, open-source framework for remote procedure calls (RPC). Here's how we can incorporate gRPC into the project:

1. **gRPC Service Definition**: Define the gRPC service and message types that will be used for communication between the servers. This can be done by creating a `.proto` file that specifies the service methods and the structure of the messages exchanged.

2. **Generate Code**: Use the gRPC compiler to generate client and server code in the desired programming language (e.g., Python, Node.js). This code will provide the necessary classes and methods for implementing the gRPC communication.

3. **Implement gRPC Server**: In each server involved in the project, implement the gRPC server by extending the generated server code. This server will handle incoming gRPC requests from other servers and execute the corresponding logic.

4. **Implement gRPC Client**: In the servers that need to communicate with other servers, implement the gRPC client by using the generated client code. This client will send gRPC requests to the target server and receive the corresponding responses.

5. **Define Service Methods**: Implement the service methods defined in the gRPC service definition. These methods will encapsulate the functionality required for inter-server communication, such as sending image or video streams, processing point clouds, and generating splats.

6. **Configure Server Endpoints**: Configure the server endpoints to expose the gRPC services. This can be done by specifying the network address and port on which the server will listen for incoming gRPC requests.

7. **Handle Error and Exception**: Handle errors and exceptions that may occur during the gRPC communication. This includes handling network failures, timeouts, and invalid requests.

By incorporating gRPC into the project, we can achieve efficient and reliable communication between the servers. gRPC provides features such as bi-directional streaming, flow control, and automatic serialization/deserialization, which can greatly simplify the implementation of inter-server communication.


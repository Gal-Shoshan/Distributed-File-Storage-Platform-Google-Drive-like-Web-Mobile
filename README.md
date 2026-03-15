# Project Drive

Welcome to Drive.
An implementation of a cloud based file storage and management.

## About:

> This project is part of the course 'Advance System Programming' at BIU.

Drive is based on the MERN full stack frameworks.

Using MVC architecture.

Including c++ files storage server.

While adhearing to SOLID principles.

Drive uses Docker to setup the internal servers needed.
And offer a react Website for the user interface, or a Native app solution using react-native.

Drive Website             |  Drive App
:-------------------------:|:-------------------------:
![](./wiki/usage%20screenshots/8.png)  |  ![](./wiki/usage%20screenshots/native-app/5.png)

## Drive Components:

Each of the following components inside Drive can be run independently.
While docker-compose will start the other necessary components.
But it is Recommanded to run one of the client for the intended usage.

### The File Server:

A basic c++ TCP server for managing files, compressing them and storing them internally.
Offer CRUD functions on the files. the server communicate only through TCP.

[Usage instructions, and more info.](./wiki/file-server.md)

### The File Server - CLI Clients:

A basic c++ and a python CLI clients for sending commands to the file server.
Offer CRUD functions on the files. communicating with the file server through TCP.

[Usage instructions, and more info.](./wiki/file-server-clients.md)

### The REST API Server:

An express server offering a full REST API for the Drive.
Utilising the file server for storing the files content, and using own MongoDB server for the metadata storage.

The REST server offer the full Drive functionalies includding creating users, and authorised access.

[Usage instructions, and more info.](./wiki/web-server.md)

### The REACT website client:

User friendly website, offering full coverage of the Drive usage.
The website is spawned in docker and offer easy browser connection.

[Usage instructions, and more info.](./wiki/drive-website.md)

### The REACT-NATIVE application client:

User friendly native application, offering full coverage of the Drive usage.
The application can be installed on the user device and offer easy Drive usage.

[Usage instructions, and more info.](./wiki/drive-native.md)
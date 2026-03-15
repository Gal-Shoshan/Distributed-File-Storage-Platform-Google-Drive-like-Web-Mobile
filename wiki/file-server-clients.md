# File server TCP clients:

While developing Drive, we developed basic TCP clients to the file server.
it helped made the file server into a independant component that we could trust.
And eventualy use as a file storage in the full Drive architacture.

## The clients:

We made two clients that talk with the file server over TCP.
One is made with c++ also.
Another with python.

Both are terminal application that uses TUI as interface.

### running the python client:

Because the "client-python" service depends on the "files-server" service
You can run this service without first running the server
docker-compose will start the server for you.

1. git clone this project.
2. make sure you are in "project-drive" directory
3. run `docker-compose run client-python`

> currently the client will run forever, stop the container to quit.

### running the c++ client:

Because the "client-cpp" service depends on the "files-server" service
You can run this service without first running the server
docker-compose will start the server for you.

1. git clone this project.
2. make sure you are in "project-drive" directory
2. run `docker-compose run client-cpp`

> currently the client will run forever, stop the container to quit.

## the CLI commands:

The clients offers a basic TUI.

They read one line, and send the command, returning the server response, and so on in a loop.

The current supported commands are:

- `POST [filename] [content (optional)]`
- `GET [filename]`
- `PATCH [filename] [content (optional)]`
- `DELETE [filename]`
- `SEARCH [query]`

## Usage example

running the python client with `docker-compose run client-python`:

![python client image](./usage%20screenshots/python.png)

running the c++ client with `docker-compose run client-cpp`:

![cpp client image](./usage%20screenshots/cpp.png)

running both clients at the same time in different terminals:

![both clients image](./usage%20screenshots/both.png)
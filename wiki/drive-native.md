# The Native app:

This is one of the full coverage clients.

It is a user friendly app that run on your device using expo go.
It is created from REACT Native, and can be fully build into a stand alone app if needed.
It offers an experiance from signup and login until file creation, edit, share, and deletion. 

## running React Native app Client:

To run the app on your device / emulator, there are a few prerequisites that need to be done.

### clone the project

0. git clone this project.
1. make sure you are in "project-drive" directory.

it is a pretty heavy image to build in docker, so make sure you have an amount of free space.

### setup local ADB server

next, in order to be compatible with all kinds of computers and docker versions.
it will require the docker host computer to have ADB server running.

the docker container will talk to the ADB server that will talk to your device / emulator.
so make sure your device is visible in your local ADB devices list.

you can check this by running `adb devices` in the computer terminal.

### setting up enviourment variables

there are two envioument variables you need to set in the docker-compose command when running the app.

**CONNAME** and **EXPO_PUBLIC_API_URL**.

### CONNAME

#### for EMULATORS:

where the CONNAME is the emualtor connection name (before the ':', without the port) given by `adb devices` command.

for example:

```
$ adb devices
List of devices attached
localhost:5555  device

```

then CONNAME will be 'localhost'.

#### for physical device:

if you are using a physical device connected through usb

then **CONNAME need to be 'localhost'**, and **not** what `adb devices` outputs.

### EXPO_PUBLIC_API_URL

because the mobile device can be run in a different ip address then the docker,
then you will need to provide the ip of the computer running the docker (docker host).

**the device and the docker host need to be under the same local network**

and the EXPO_PUBLIC_API_URL is the local ip (of the same network) of the computer running the docker services.

can be seen with the command `ifconfig` on linux. `ipconfig` on windows.

for example EXPO_PUBLIC_API_URL can be '10.0.0.1'

### the command to run

there is two Commands possible, depends on the os you are running with.

on **Windows** the command to run the service is:

```
$env:CONNAME="[emulator-connection-name]"; $env:EXPO_PUBLIC_API_URL="[docker-host-ip]"; docker-compose up "react-native-app"
```

on **linux** the command will be **it should be a single line without ; or &&**: 

```
CONNAME="[emulator-connection-name]" EXPO_PUBLIC_API_URL="[docker-host-ip]" docker compose up "react-native-app"
```

3. you should see 'expo go' being installed on your device if it wasnt installed already.
4. then you should see the app being built in expo go, and opened.
5. use the app within the same network as the computer with the docker. (or it could hang waiting to connect)

## Usage Example:

creating an account

![q](./usage%20screenshots/native-app/1.png)
![q](./usage%20screenshots/native-app/2.png)

login in

![q](./usage%20screenshots/native-app/3.png)

creating a file and a folder

![q](./usage%20screenshots/native-app/4.png)
![q](./usage%20screenshots/native-app/5.png)

file menu options

![q](./usage%20screenshots/native-app/6.png)

sharing the file with others

![q](./usage%20screenshots/native-app/7.png)
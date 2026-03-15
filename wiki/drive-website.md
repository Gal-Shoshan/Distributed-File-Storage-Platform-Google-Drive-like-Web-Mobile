# The React website:

This is one of the full coverage clients.

It is a user friendly website run in docker, that can be accessed in the browser in the docker ip address.
This is a separate docker-compose service that utilize the REST API at the web-server service.
It offers an experiance from signup and login until file creation, edit, share, and deletion. 

## running React WebSite Client:

to run the Website (service "google-drive"):

because the "google-drive" service depends on the "web-server" service
you can run this service without first running the web server
docker-compose will start the web server for you.

0. git clone this project.
1. make sure you are in "project-drive" directory.
2. run `docker-compose up "google-drive"`.
3. open browser at "http://localhost:8980" (or docker-host ip if ran remotely).
4. use the site **for proper usage use chrome based browsers**

## Usage Example:

signing up

![q](./usage%20screenshots/1.png)

creating a file

![q](./usage%20screenshots/2.png)
![q](./usage%20screenshots/4.png)

user info

![q](./usage%20screenshots/3.png)

sharing a file with other users

![q](./usage%20screenshots/5.png)
![q](./usage%20screenshots/6.png)
![q](./usage%20screenshots/7.png)

editing files shared with you

![q](./usage%20screenshots/8.png)
![q](./usage%20screenshots/9.png)
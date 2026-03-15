# The REST API express server:

This Component is a JSON REST server running on express, using the MVC architecture.
It uses the file server as the files content storage, and a mongoDB as the metadata storage.

Its the server that fully offer all of the drive capabilities.

## Running the web server:

to run the Server (service "web-server"):

because the "web-server" service depends on the "files-server" service
you can run this service without first running the files server
docker-compose will start the files server for you.

0. git clone this project.
1. make sure you are in "project-drive" directory.
2. run `docker-compose up web-server`.
3. send http request for port 3000. if local docker than ip is 'localhost'. (more in api usage below...)

the `up` command will not allow you to interact with the files-server via the terminal. (unless attached).
but if you require it, the command `run` will run it with terminal IO
but the service that way will not serve the clients.

## The web server REST API usage:

<details>
 <summary>REST API usage.</summary>
 </br>

the API is divided into tree main concepts to interact with:

users, files, permissions

### users:

the api for users allows requests for:

#### create a new user-

send a http `POST` request to the endpoint `api/users`.
with a request body containing the following JSON.

```
{
    "fullName": "...",
    "username": "...",
    "password": "...",
    "picture": "...",
    "email": "..."
}
```

#### get existing user data-

send a http `GET` request to the endpoint `api/users/:id`,
where `:id` is the id of the existing user.

#### check user exist in the server-

send a http `GET` request to the endpoint `api/tokens`.
with a request body containing the following JSON.

```
{
    "username": "...",
    "password": "..."
}
```

it will return the user id if he exist in the server.

### files:

the api for files/folders manipulation allows requests for:

#### create a new file/folder-

send a http `POST` request to the endpoint `api/files`.
with a request body containing the following JSON.

```
{
    "userId": "...",
    "FType": "...",
    "FName": "...", 
    "FContent": "..."
}
```

where the "userId" is the 'logged in' user id.
and "FType" is either :

- "Folder"
- or "File"

"Fname" is the name for the file/folder to create.
"FContent" is the content of the file to create.

> if "FType" is "Folder" than **dont** add "FContent". it will be considered a Bad request.

#### see all users files/folders-

send a http `GET` request to the endpoint `api/files`.
with a request body containing the following JSON.

```
{
    "userId": "..."
}
```

where the "userId" is the 'logged in' user id.

#### search all users files/folders-

send a http `GET` request to the endpoint `api/search/:query`,
where `:query` is the string to search in the files/folders name or content.
with a request body containing the following JSON.

```
{
    "userId": "..."
}
```

where the "userId" is the 'logged in' user id.

#### see user specifiec file/folder-

send a http `GET` request to the endpoint `api/files/:id`,
where `:id` is the id of the file/folder.
with a request body containing the following JSON

```
{
    "userId": "..."
}
```

where the userId is the 'logged in' user id.

#### update user specifiec file/folder-

send a http `PATCH` request to the endpoint `api/files/:id`,
where `:id` is the id of the file/folder.
with a request body containing the following JSON.

```
{
    "userId": "...",
    "FName": "...", 
    "FContent": "..."
}
```

where the "userId" is the 'logged in' user id.
"Fname" is the name for the file/folder to create.
"FContent" is the content of the file to create.

#### delete user specifiec file/folder-

send a http `DELETE` request to the endpoint `api/files/:id`,
where `:id` is the id of the file/folder.
with a request body containing the following JSON.

```
{
    "userId": "..."
}
```

where the userId is the 'logged in' user id.

### permissions:

the api for user files/folders permission manipulation allows requests for:

#### create a new file/folder permission-

send a http `POST` request to the endpoint `api/files/:id/permissions`.
where `:id` is the file id.
with a request body containing the following JSON

```
{
    "userId": "...",
    "users": ["...", "...", ...],
    "flags": ["...", "...", ...]
}
```

where the "userId" is the 'logged in' user id.
the "users" are the users id to allow the flags. (logicly good usage will be only allow one user at a time... but it does support multiple)
the "flags" are the permission for the file/ folder.
the current flags that have effect are:

- "get" allows the other user to read and search the file/folder
- "patch" allows to modify the file/folder
- "delete" allows to delete the file/folder

#### get all of the file/folder permissions-

send a http `GET` request to the endpoint `api/files/:id/permissions`.
where `:id` is the file id.
with a request body containing the following JSON

```
{
    "userId": "..."
}
```

where the "userId" is the 'logged in' user id.

#### update a specific file/folder permission-

send a http `PATCH` request to the endpoint `api/files/:id/permissions/:pid`.
where `:id` is the file id.
and the `:pid` is the specific permission id.
with a request body containing the following JSON

```
{
    "userId": "...",
    "users": ["...", "...", ...],
    "flags": ["...", "...", ...]
}
```

where the "userId" is the 'logged in' user id.
the "users" are the users id to allow the flags. (logicly good usage will be only allow one user at a time... but it does support multiple)
the "flags" are the permission for the file/ folder.
the current flags that have effect are:

- "get" allows the other user to read and search the file/folder
- "patch" allows to modify the file/folder
- "delete" allows to delete the file/folder

#### delete a specific file/folder permission-

send a http `DELETE` request to the endpoint `api/files/:id/permissions/:pid`.
where `:id` is the file id.
and the `:pid` is the specific permission id.
with a request body containing the following JSON

```
{
    "userId": "..."
}
```

where the "userId" is the 'logged in' user id.

</details>

## Usage Examples:

using the web server api part 1:

**some JSON fields names were changed**, see the API usage for current json names.

![api-usage-1](./usage%20screenshots/api-usage-1.png)

using the web server api part 2:

**some JSON fields names were changed**, see the API usage for current json names.

![api-usage-2](./usage%20screenshots/api-usage-2.png)
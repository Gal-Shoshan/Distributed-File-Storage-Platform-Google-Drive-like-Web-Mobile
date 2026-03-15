# c++ TCP file server

This is a component part of the Drive.

The file server is a docker-compose service.
and so need to be run through docker-compose.

## running the files server:

to run the Server (service "files-server"):

1. git clone this repository.
2. make sure you are in "project-drive" directory.
3. run `docker-compose up files-server`

the `up` command will not allow you to interact with the files-server via the terminal. (unless attached).
but if you require it, the command `run` will run it with terminal IO
but the service that way will not serve the clients.

## tests for the file server:

This component was developed with TDD. with the GTEST library.
and so if you want to run the tests yourself you can.

### running tests for files-server:

to test the files-server:

1. make sure you are in "project-drive" dir
2. run `docker-compose run gtest`

> running docker build in the /test folder wont work. test only by docker-compos in the root project folder.

#### tests example

running the Server tests with `docker-compose run gtest`:

![tests image](./usage%20screenshots/tests.png)

## code structure UML for the files-server:

this diagrem is the current structure of the app classes

```mermaid
---
title: Project-Drive
---
classDiagram
    class main{
        +main()
    }
    class App{ 
        App : -menu IMenu*
        App : -commandsMap Map<string, ICommand*>
        App : -inputOutput IInputOutput*
        +App(IMenu* menu, std::map<std::string, ICommand* > commandsMap, IInputOutput* inputOutput)
        +run()
    }
    class AppTools{
        +stringIntoArgs(string rawString) Vector<string>
        +argsIntoString(vector<string> args) String
    }
    class IThread{
        <<interface>>
        +AddTask(clientsock, App& app) void
    }
    class Thread{
        +AddTask(clientsock, App& app) void
        +endOfTask(clientSock)
    }
    class ThreadPool{
        +AddTask(clientsock, App& app) void
        +endOfTask(clientSock)
    }
    class IMenu{
        <<interface>>
        IMunu : -inputOutput IInputOutput*
        +nextCommand() String
        +displayError(string) Void
    }
    class EmptyMenu{
        EmptyMenu : -rawInput String
        EmptyMenu : -IO Unique_ptr<CliIO>
        +EmptyMenu(IInputOutput* inputOutput)
        +nextCommand() String
        +displayError(string str) Void
    }
    class ICommand{
        <<interface>>
        +execute()
    }
    class AddFileCommand{
        AddFileCommand : -compressor Unique_ptr<Compressor>
        AddFileCommand : -storagePath String
        -splitRawCommand(std::string rawCommand) Vector<string>
        +AddFileCommand()
        +execute(string rawCommand) Vector<String>
    }
    class GetFileCommand{
        GetFileCommand : -compressor Unique_ptr<Compressor>
        GetFileCommand : -storagePath String
        -splitRawCommand(std::string rawCommand) Vector<string>
        +GetFileCommand()
        +execute(string rawCommand) Vector<string>
    }
    class Search{
        +Search()
        +execute(string command) Vector<string>
        -SearchInFile(string file, string substr) String
        -GetContent(string command) String
    }
    class Delete{
        +Delete()
        +execute(string command) Vector<string>
        -ValidContent(string command) Bool
        -GetPath(string file_name) Filesystem :: path
        -FileExist(string file_name) Bool
    }
    class IInputOutput{
        <<interface>>
        IInputOutput : -format IPrintFormat*
        +input(int source) String
        +output(int dest, string s) Void
    }
    class CliIO{
        +CliIO(IPrintFormat* format)
        +input(int source) String
        +output(int dest, string s) Void
    }
    class SocketIO{
        +SocketIO(IPrintFormat* format)
        +input(int source) String
        +output(int dest, string s) Void
    }
    class Compressor{
        +Compressor ()
        +compressFile(String s) String
        +decompressFile(String s) String
    }
    class IPrintFormat{
        +PrintFormat String
    }
    class SecTaskPrintFormat{
        +SecTaskPrintFormat()
        +PrintFormat String
    }
    main --* App
    App --* IMenu
    App --* ICommand
    App --* AppTools
    App --* IThread
    IMenu --* IInputOutput
    IInputOutput --* IPrintFormat
    App -- IInputOutput
    IThread <|-- Thread
    IThread <|-- ThreadPool
    IMenu <|-- EmptyMenu
    ICommand <|-- AddFileCommand
    ICommand <|-- GetFileCommand
    ICommand <|-- Search
    ICommand <|-- Delete
    IInputOutput <|-- CliIO
    IInputOutput <|-- SocketIO
    IPrintFormat <|-- SecTaskPrintFormat
    AddFileCommand --* Compressor
    GetFileCommand --* Compressor
    Search --* GetFileCommand
```
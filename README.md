FISH-Centralized-FIle-SHaring
=============================

FISH--FIle-SHaring
==================

FISH: FIle SHaring, a Distributed File System

"Truth is out there"

'FISH' is a file sharing system allowing its users to share media files (such as MP3 and images) on the Internet. Since it has been started, it has known a huge success, in such an extent that some universities have been forced to forbid their students to use FISH on their networks.

You may have recently heard or read about FISH since the trial it lost against some music publishing companies have been one of last summer's success story. Have you already wondered how such a system can work?


The Architecture
==================

The FISH distributed file system can be structured in two different ways explained below.

Structure One: Centralized Server (For the Decentralized version please look here:)

The FISH can be based on two components: (1) one central FISH server,  (2) and many FISH clients (Although the term 'client' is not accurate here, as we shall see later). The server is run on a computer  with known DNS name, while the clients run on users' computers.

Each user may possess some files on his hard drive, and may share them with all the other users via the FISH's server. Clients start by contacting the server and send it a list of the files the client is sharing. The server manages a directory (list) of shared files and associated addresses of clients. If a client exits or crashes, the server should remove records corresponding to the client from the directory. To achieve this, the server should have a mechanism to detect crashed or exited clients.

Clients may query the server to know if a given file is currently shared by another user. The server should reply by either a 'not found' message, or by giving the address of the client(s) that is(are) sharing the file. If the file is available, the requesting client may connect to the client that shares the file, and download the file.

Thus, the term 'client' is not appropriate since the clients are at the same time file servers. Despite this lack of accuracy, we will keep on using this term to name the program used by FISH users on their computer.

Goal
==================

To use Thread, Socket, ServerSocket, Input and OutputStream, StringTokenizer and other utility classes.

Step 1: Client listing shared files
===
Develop a Java application Client containing a method main() that can take the three following arguments: the path to a directory containing files to be shared, the address and the port of the FISH server to be connected to. The Client command line should look like:

java Client [shared_file_path] [server_address] [server_port]

If some arguments are missing,  Client should use default values. It is especially advised to use localhost as the default address of the server.

Client gets a list of the files located in the shared_file_path directory, and stores the names of the files that are 'shareable' into some Java structure. For convenience, we assume that any readable file that is not a directory can be shared. Errors should be displayed.

Tips:

Read the API documentation for java.io.File.
Read about arrays, and the API documentation for java.util.Vector, java.util.LinkedList, and java.util.Hashtable.
Option:
Consider sharing files located in subdirectories of shared_file_path.
Step 2: Client-Server protocol
Design a protocol with messages for the following interactions:

A client registers at the server by sending a list of shared file names.
A client sends to the server a search request for a specific filename.
The server replies to the requesting client by sending either a 'not found' message or addresses of client(s) sharing the requested file.
The client unregisters at the server (when the client stops sharing files).
Option:
You are free to invent other messages, such as the server telling the client how many files are currently shared, or how many clients are currently registered.
Step 3: Client File Sharing
To implement parts of the protocol defined at Step 2, define two methods in Client: 
- a method share() that registers the client at the server and sends the server a list of shared file names. 
- a method unshare() that tells the server to remove from the server all names of the files shared by this client and to unregister the client.

Use java.net.Socket for client-server communication.

Tips:

Read the API documentation for InputStream, InputStreamReader, BufferedReader, OutputStream, OutputStreamWriter, PrintWriter. (See Java SE API documentation)
Look at Example 3.5: A finger client.
Step 4: Client User Interface and Command Interpreter
Extend the code of method main() in Client to make it call share(), before starting a simple command line User Interface (UI) that reads user commands and initiates their execution. For each command entered by the user, the UI should output the result of the command or an error message. At this stage, you should just implement a command 'exit', which should make the client call unshare() and stop. This UI will be extended later to support querying the server for shared files.

Tips:

For system IO, read the API documentation for java.lang.System.
For string parsing, you may read about java.util.StringTokenizer.
Inspect the Client in the Bank example that  illustrates a command UI.
Step 5: Server managing a directory of shared file names
Develop a Server waiting for connections from clients and creating a thread to handle each new connection. This thread should read the data sent by the client and recognize the type of message received, according to the protocol designed at Step 2. When a message corresponds to sharing or unsharing files, the server should update its directory (a 'kind of database' of names of shared files and their locations) by adding or removing the corresponding filenames. 
The design of the directory is an important issue. The directory  should provide a mapping of filenames to clients IP addresses and port numbers. The directory should allow to search (lookup) for filenames. You should provide efficient search algorithm, as the directory might become large. Keep in mind that the directory you developed in Sub-assignment 1 should be reused in Sub-assignment 2, where it should allow searching not only entire filenames but also keywords.

The server's port number can be specified as a command line argument. If the port was not specified, the Server should use a default port number. The server should keep track of registered clients and available shared files, and should be able to provide this information on a client request.

Step 6: Debug and Run

Start Server and Client, try to share and unshare files with the Client, and optionally to retrieve statistics from the server. Try to run more then one client clients.

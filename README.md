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


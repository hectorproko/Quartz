# Distributed File System
- Distributed File System (DFS) refers to a set of client and server services that allow an organization to organize many distributed [[SMB (Server Message Block) protocol|SMB]] file shares into a distributed file system.
- Distributed File System (DFS) is primarily a <mark style="background: #ADCCFFA6;">Microsoft Windows Server</mark> feature

## There are two main technologies within DFS:

### DFS Namespaces: 
This allows you to group shared folders located on different servers into one or more logically structured namespaces. This makes it possible to access and manage multiple file servers and shares as if they were one file system.

### DFS Replication: 
This is an optional feature that you can use to replicate the data in DFS. DFS Replication uses a compression algorithm known as remote differential compression (RDC) to replicate only the changes to the data, thereby saving bandwidth.
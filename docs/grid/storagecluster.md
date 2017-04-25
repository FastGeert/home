# G8OS Storage Cluster

The G8OS storage cluster consists of multiple connected key-value stores (default is ARDB) spread over the G8OS nodes.

Creating a storage cluster can be achieved through the Grid API.

The storage cluster is used by:
- [NBD Servers](#nbd)
- [TLOG Servers](tlog)
- [NAS Servers](nas)
- [S3 Servers](s3)

<a id="nbd"></a>
## NBD Servers

NBD, abbreviation for Network Block Device, is the lightweight block access protocol used in a G8OS grid to implement block storage.

A NBD Server actually implements the NBD protocol. For each virtual machine that needs block storage one NBD Server is required.

Each of these NBD Severs, or volume driver servers, runs in a container, and depend on another container that implements the TLOG Server.

![Architecture](block-storage-architecture.png)

<a id="tlog"></a>
## TLOG Servers

- Compresses and encrypts
- Cuts files of +1MB in file parts of <1MB (SCO's)
- Stores data to G8OS ObjStor (HDD)
- Stores metadata into GIG Directory Service
- Puts the hashes to the blockchain


<a id="nas"></a>
## NAS Servers


<a id="s3"></a>
## S3 Servers

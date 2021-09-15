# **SystemsExpert Video Notes**

- [**SystemsExpert Video Notes**](#systemsexpert-video-notes)
  - [**01 - Design Fundamentals - Introduction**](#01---design-fundamentals---introduction)
  - [**02 - What Are Design Fundamentals?**](#02---what-are-design-fundamentals)
    - [**4 Categories of Design Fundamentals**](#4-categories-of-design-fundamentals)
  - [**03 - Client/Server Model**](#03---clientserver-model)
  - [**04 - Network Protocols**](#04---network-protocols)
  - [**05 - Storage**](#05---storage)
  - [**06 - Latency and Throughput**](#06---latency-and-throughput)
  - [**07 - Availability**](#07---availability)

## **01 - Design Fundamentals - Introduction**

Design Fundamentals are necessary to tackle of Systems Design Interview.

## **02 - What Are Design Fundamentals?**

- What kind of system are we building?
- What kind of functionality is our system going to support?
- What characteristics will be value in our system?
- There is a lot of subjectivity to Systems Design solutions

### **4 Categories of Design Fundamentals**

1. ***Underlying/Foundational Knowledge***
    1. Design fundamentals such that if you don't have sufficient knowledge to understand these, you will at best
      at best have gaps in your knowledge that will undermine your decisions, and at worst make you incapable of beginning
      to tackle a Systems problem
    2. **The Client/Server Model**
    3. **Network Protocols**
2. ***Key Characteristics of Systems***
   1. Characteristics that systems may have and trade-offs you might make
   2. **Availability**
   3. **Latency**
   4. **Throughput**
   5. **Redundancy**
   6. **Consistency**
3. ***Actual Components of a System***
   1. The key components that are going to allow your system to have key characteristics above
   2. **Load Balancers**
   3. **Proxies**
   4. **Caches**
   5. **Rate Limiting**
   6. **Leader Election**
4. ***Actual Technology***
   1. **Zoo Keeper**
   2. **Nginx**
   3. **Reddis**
   4. **AWS S3**
   5. **Google Cloud Storage**

## **03 - Client/Server Model**

1. **Key Terms**
   1. **Client**
      1. A machine or process that requests data or service from a server.
      2. Note that a single machine or piece of software can be both a client and a server at the same time.  For instance, a single machine
          could act as a server for end users and as a client for a database
   2. **Server**
      1. A machine or process that provides data or service for a client, usually by listening for incoming network calls
      2. Note that a single machine or piece of software can be both a client and a server at the same time.  For instance, a single machine
          could act as a server for end users and as a client for a database
   3. **Client/Server Model**
      1. The paradigm by which modern systems are designed, which consists of clients requesting data or service from servers, and servers providing
          data or service to clients
   4. **IP Address**
      1. An address given to each machine connected to the public internet.  IPv4 addresses consist of four numbers separated by dots: `a.b.c.d.`
          where all four numbers are between 0 and 255.  Special values include:
          1. `127.0.0.1` - Your own local machine, referred to as **localhost**
          2. `192.168.x.y` - Your private network.  For instance, your machine and all machines on your private wifi network will usually have this prefix
      2. You can think of an IP Address kind of like a mailbox, which can receive mail (connections), and send mail (connections)
   5. **Port**
      1. In order for multiple programs to listen for new network connections on the same machine without colliding, they pick a **port number** to listen on.
      2. A port is an integer between 0 and 65,535(2¹⁶ ports total)
      3. Typically, ports 0-1023 are reserved for *system ports* (also called *well-known ports*) and shouldn't be used by user-level processes.
          Certain ports have pre-defined uses, and although you usually won't be required to have them memorized, they can sometimes come in handy:
          1. `22`: Secure Shell
          2. `53`: DNS lookup
          3. `80`: HTTP
          4. `443`: HTTPS
      4. Ports can be thought of as the mailbox numbers of an apartment complex, where the apartment complex is the IP Address
   6. **DNS**
      1. Short for **Domain Name System**, it describes the entities and protocols involved in the translation from domain names to IP Addresses.
          Typically, machines make a **DNS Query** to a well known entity, which is responsible for returning the IP Addresses (or multiple one)
          of the requested domain name in the response
2. What happens when you put a URL in your browser and hit enter
   1. **Client** is your browser (machine)
   2. **Server** is what you're requesting data from (machine)
   3. **Browser** checks cache to see if you've ever been there before.
      1. If you have and you have data caching, it will load saved information and likely have the **IP Address**
   4. If not, the **Browser** (Client) makes a **DNS Query** to Server's **Domain Name** to get an **IP Address**
      1. A DNS query can be emulated by using the `dig` terminal command on Ubuntu: `dig appacademy.io`
   5. The **Domain Name System** return the **IP Address**, to which the **Browser** (client) sends a **HTTP Request** for data
   6. The **IP Address** (Server) will handle the **HTTP Request** the best it can, and will generate a **HTTP Response** to send back to the **Browser** (Client)
   7. You can simulate this experience by opening two Ubuntu Terminals:
      1. In one terminal type `nc -l 8081` (NetCat Listen on 8081)
      2. In the other terminal type `nc 127.0.0.1 8081`
      3. This simulates a connection between the two terminals.  Anything typed in the one where you're listening will echo to the other

## **04 - Network Protocols**

1. **Key Terms**
   1. **IP**
      1. Stands for **Internet Protocol**.  This network protocol outlines how almost all machine-to-machine communications should happen in the world.
          **TCP**/**UDP**/**HTTP** are built on top of **IP**
   2. **TCP**
      1. Stands for **Transmission Control Protocol**. Network protocol built on top of the **Internet Protocol (IP)**.  Allows for ordered,
          reliable data delivery between machines over the public internet by creating a **connection**
      2. **TCP** is usually implemented in the kernel, which exposes **sockets** to applications that they can use to stream data through an open connection.
         1. The process is similar to a handshake:
            1. A client reaches out to a server an requests to make a connection
            2. The server accepts/rejects and reaches out to the client with it's response
            3. The client creates an open connection with the server
         2. Connections can timeout with inactivity
         3. Either client or server can end the connection at any point
      3. **IP Packets** can also contain **TCP Headers**
   3. **HTTP**
      1. The **H**yper**T**ext **T**ransfer **P**rotocol is a very common network protocol implemented on top of TCP.  Clients make **HTTP Requests**,
          and servers respond with an **HTTP Response**
         1. **I**nternet **P**rotocol is the foundation.
         2. **T**ransmission **C**ontrol **P**rotocol is built on top of **IP**
         3. **H**yper**T**ext **T**ransfer **P**rotocol is built on top of **TCP**
      2. Requests typically have the following schema:

         ```http
         host: string (example: algoexpert.io)
         port: integer (example: 80/443)
         method: string (example: GET, POST, PUT, PATCH, DELETE, OPTIONS)
         headers: pair list (example: "Content-Type" => "application/json")
         body: opaque sequence of bytes
         ```

      3. Responses typically have the following schema:

         ```http
         status code: integer (example: 200, 404)
         headers: pair list (example: "Content-Length" => 1234)
         body: opaque sequence of bytes
         ```

   4. **IP Packet**
      1. Sometimes more broadly referred to as just a (network) **packet**, an IP packet is effectively the smallest unit used to describe data being sent
          over IP, aside from bytes.  An IP packet consists of:
         1. An **IP Header**, which contains the source and destination **IP Addresses** as well as other information related to the network
            1. Between 20-60 bytes
         2. A **payload**, which is just the data being sent over the network
      2. Only 2¹⁶ bytes (65k bytes)
   5. **Protocol**
      1. An agreed upon set of rules for an interaction between two parties

## **05 - Storage**

1. **Key Terms**
   1. **Databases**
      1. Databases are programs that either use disk or memory to do 2 core things.  **Record** data and **Query** data.  In general, they are themselves
          servers that are long lived and interact with the rest of your application through network calls, with protocols on top of TCP and even HTTP
      2. Some databases only keep records in memory, and the users of such databases are aware of the fact that those records may be lost forever
          if the machine or process dies
      3. For the most part though, databases need persistence of those records, and thus cannot use memory. This means that you have to write your data
          to disk.  Anything written to disk will remain through power loss or network partitions, so that's what is used to keep permanent records.
      4. Since machines die often in a large scale system, special disk partitions or volumes are used by the database processes, and those volumes
          can get recovered even if the machine were to go down permanently
   2. **Disk**
      1. Usually refers to either **Hard-Disk Drives (HDD)** or **Solid-State Drives(SSD)**.  Data written to disk will persist through power failures and general
          machine crashes.  Disk is also referred to **non-volatile storage**
      2. **SSD** is far faster than **HDD** (See latencies of accessing data from SSD and HDD, but also far more expensive from a financial point of view.
          Because of that, HDD will typically be used for data that's rarely accessed or updated, but that's stored for a long time, and SSD will be used for
          data that's frequently accessed and updated.
   3. **Memory**
      1. Short for **Random Access Memory (RAM)**.  Data stored in memory will be lost when the process that has written that data dies.
   4. **Persistent Storage**
      1. Usually refers to disk, but in general it is any form of storage that persists if the process in charge of managing it dies

## **06 - Latency and Throughput**

1. **Key Terms**
   1. **Latency** and **Throughput** are the two most important measures of the performance of a system.  They are not correlated.
   2. **Latency** - How long does it take data to get from one point in a system to another point in a system
      1. The time it takes for a certain operation to complete in a system.  Most often this measure is a time duration, like milliseconds or seconds.
          You should know these orders of magnitude:
          1. Reading 1 MB from RAM: 250 µs (0.25 ms - microseconds)
          2. Reading 1 MB from SSD: 1,000 µs (1 ms)
          3. Transfer 1 MB over 1 GB/s Network: 10,000 µs (10 ms)
          4. Reading 1 MB from HDD: 20,000 µs (20 ms)
          5. Inter-Continental Road Trip: 150,000 µs (150 ms)
   3. **Throughput**
      1. The number of operations that a system can handle properly per time unit.  For instance the throughput of a server can often be measured
          in **requests per second** (**RPS** or **QPS**)

## **07 - Availability**

1. **Key Terms**
   1. **Availability**
      1. The odds of a particular server or service being up and running at any point in time, usually measured in **percentages**.  A server
          that has 99% availability will be operational 99% of the time (this would be described as having two **nines** of availability)
   2. **High Availability**
      1. Used to describe systems that have particularly high levels of availability, typically 5 **nines** or more
      2. Sometimes abbreviated **"HA"**
   3. **Nines**
      1. Typically refers to percentages of uptime.  For example, 5 **nines** of availability means an uptime 99.999% of the time.
      2. Downtimes expected per year depending on **nines**:
         1. 99% (2 nines): 87.7 hours
         2. 99.9% (3 nines): 8.8 hours
         3. 99.99% (4 nines): 52.6 minutes
         4. 99.999% (5 nines): 5.3 minutes
   4. **Redundancy**
      1. The process of replicating parts of a system in an effort to make it more reliable
   5. **Service-Level Agreement (SLA)**
      1. A collection of guarantees given to a customer by a service provider.  SLAs typically make guarantees on a system's availability, amongst other things.
      2. Made up of multiple SLOs
   6. **Service-Level Objective (SLO)**
      1. A guarantee given to a customer by a service provider.  SLOs typically make guarantees on a system's availability, amongst other things.
      2. SLOs constitute an SLA
   7. **Process**
      1. A program that is currently running on your machine.  You should always assume that any process may get terminated at any time in a sufficiently large system
   8. **Node/Instance/Host**
      1. These three terms refer to the same thing most of the time: A virtual or physical machine on which the developer runs processes.
      2. Sometimes the word server also refers to the same concept
   9. **Redundancy**
      1. Concept - Duplication of critical data or services with the intention of increased reliability and availability of the system.
      2. Server Failover - Remove single points of failure and provide backups (e.g. server failover)
      3. Shared-nothing Architecture
         1. Each node can operate independently of one another
         2. No central service managing state or orchestrating activities
         3. New servers can be added without special conditions or knowledge
         4. No single point of failure
      4. [Models of Redundancy] (https://www.ni.com/ja-jp/innovations/white-papers/08/redundant-system-basic-concepts.html)
      5. Standby Redundancy
         1. Standby redundancy, also known as **Backup Redundancy** is when you have an identical secondary unit to back up the primary unit,
             The secondary unit typically does not monitor the system but is there just as a spare
         2. The standby unit is not usually kept in sync with the primary unit, so it must reconcile it's I/O signals on the takeover of the
             **Device Under Control (DUC)**
         3. You also need a third party to be a watchdog, which monitors the system to decide when a switchover condition is met and command the
             system to switch control to the standby unit and a voter
         4. In standby redundancy, there are two basic types, **Cold Standby** and **Hot Standby**
            1. Cold Standby - The secondary unit is powered off, thus preserving the reliability of the unit, so it takes time to bring it online
                and it makes it more challenging to reconcile synchronization issues
            2. Hot Standby - The secondary unit is powered up and can optionally monitor the DUC.  It can also be used as the watchdog and/or voter
                to decide when to switch over.  It shortens the downtime, which in turn increases availability in your system.
      6. N Modular Redundancy
         1. N Modular Redundancy, also known as **Parallel Redundancy**, refers to the approach of having multiple units running in parallel.
         2. All units are highly synchronized and receive the same input information at the same time.
         3. Their output values are then compared and a voter decides which output values should be used. This model easily provides bumpless switchovers
         4. This model typically has faster switchover times than Hot Standby models, but the system is more at risk of encountering a common node
             failure across all units
         5. In N Modular Redundancy, there are three main typologies:
            1. **Dual Modular Redundancy (DMR)** - Uses two functional equivalent units, thus either can control the DUC.
            2. **Triple Modular Redundancy (TMR)** - Uses three functionally equivalent units to provide redundant backup
            3. **Quadruple Modular Redundancy (QMR)** - Uses four functionally equivalent units to provide redundant backup
      7. 1:N Redundancy
         1. 1:N is a design technique used where you have a single backup for multiple systems and this backup is able to function in the place of any
             single one of the active systems.  This technique offers redundancy at a much lower cost than the other models by using one standby unit
             for several primary units
         2. This approach only works well when the primary units all have very similar functions, thus allowing the standby to back up any of the
             primary units if one of them fails
         3. The drawbacks of this approach are added complexity of deciding when to switch and of a switch matrix than can reroute signals correctly and efficiently
   10. **Redundancy At Different Layers**
       1. **Network Redundancy**
          1. Layer 2 Redundancy (switches)
             1. Active/Standby using Spanning Tree Protocol
             2. Active/Active using per VLAN spanning tree protocol and Multiple Spanning Tree Protocol
          2. Layer 3 Redundancy
             1. First Hop Redundancy Protocols are designed to provide redundancy to clients by representing multiple default gateways in a group with a single IP
       2. **VM/Server Redundancy**
          1. **VMware HA** provides high availability for virtual machines by pooling them and the hosts they reside on into a cluster.  Hosts in the cluster are
              are monitored and in the event of a failure, the virtual machines on a failed host are restarted on alternate hosts.
          2. **Primary and Secondary Hosts in a VMware HA Cluster**
             1. When you add a host to a VMware HA cluster, an agent is uploaded to the host and configured to communicate with other agents in the cluster.
             2. The first five hosts added to the cluster are designated as primary hosts, and all subsequence hosts are designated as secondary hosts
             3. The primary hosts maintain and replicate all cluster state and are used to initiate failover actions
             4. If a primary host is removed from the cluster, VMware HA promotes another (secondary) host to primary status
             5. If a primary host is going to be offline for an extended period of time, you should remove it from the cluster, so that it can be replaced.
             6. Any host that joins the cluster must communicate with an existing primary host to complete it's configuration, except when adding first host
             7. At least one primary host must be functional for VMware HA to operate correctly
             8. If all primary hosts are unavailable (not responding), no hosts can be successfully configured for VMware HA.  You should consider this limit
                 of five primary hosts per cluster when planning the scale of your cluster.
             9. One of the primary hosts is also designated as the active primary host and it's responsibilities include:
                1. Deciding where to restart virtual machines
                2. Keeping track of failed restart attempts
                3. Determining when it is appropriate to keep trying to restart a virtual machine
             10. If the primary host fails, another primary host replaces it.
       3. **Database Redundancy**
          1. Have more than one copy of your data in a database system.  It can either be at the table level or the field level.  Usually, copies are called **replica**
          2. e.g. Replicas in ClustrixDB are distributed across the cluster for redundancy and to balance read, writes, and disk usage.
       4. **Storage Redundancy**
          1. [Azure Storage Redundancy](https://www.petri.com/understanding-azure-storage-storage-types-redundancy)
          2. **Locally Redundant Storage (LRS)**
             1. LRS ensures that your data stays within a single data center in your chosen region.  Data is replicated three times.  LRS is cheaper than the other types
                 of redundancy and doesn't provide protection against data center failures
          3. **Zone-Redundant Storage (ZRS)**
             1. Only available for block blobs, ZRS keeps three copies of your data across two/three data centers, either within your region or across two regions
          4. **Geo-Redundant Storage (GRS)**
             1. This is the type of redundancy that Microsoft recommends by default, and it keeps six copies of your data.  Three copies stay in the primary region, and
                 the remaining three are replicated to a secondary region
          5. **Read-Access Geo-Redundant Storage (RA-GRS)**
             1. The default redundancy setting, RA-GRS replicates data to a secondary region, where apps also get read access to the data
          6. **Application Redundancy**
             1. Redundant applications, normally server applications, provide backup capability in the event that the application fails.  That is, if one server
                 (the primary server) goes out of service for some reason, such as lost connectivity, the other server (the backup server) can act as the primary
                 server, with little or no loss of service
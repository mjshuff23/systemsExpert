# **SystemsExpert Video Notes**

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
   5. The **Domain Name System** return the **IP Address**, to which the **Browser** (client) sends a **request** for data
   6. The **IP Address** (Server) will handle the **request** the best it can, and will generate a **response** to send back to the **Browser** (Client)

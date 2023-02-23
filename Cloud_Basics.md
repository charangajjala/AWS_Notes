
`Recommended concepts for undertanding the cloud better `. 

# Cloud Basics

**Topics**:
- [Cloud Basics](#cloud-basics)
  - [Virtualization](#virtualization)
    - [Physial Machine](#physial-machine)
    - [Virtual Machine](#virtual-machine)
    - [Physical Server](#physical-server)
    - [Virtual Server](#virtual-server)
    - [Does virtual server exist only in a virtual machine?](#does-virtual-server-exist-only-in-a-virtual-machine)
    - [Can a single virtual machine have multiple virtual servers?](#can-a-single-virtual-machine-have-multiple-virtual-servers)
    - [Can a physical machine run more than one server?](#can-a-physical-machine-run-more-than-one-server)
    - [Can a virtual machine has more than one os?](#can-a-virtual-machine-has-more-than-one-os)
    - [Summary of these concepts](#summary-of-these-concepts)
  - [Networks](#networks)
    - [Network Traffic/Protocols](#network-trafficprotocols)
  - [Network File System (NFS)](#network-file-system-nfs)
  - [Application Servers, Sessions, Caches](#application-servers-sessions-caches)
    - [Sessions](#sessions)
    - [Cache](#cache)


## Virtualization
### Physial Machine
- A physical machine refers to a standalone computer or server that is not part of a virtualized environment.  
- It is a physical, standalone device that consists of hardware components such as a central processing unit (CPU), memory (RAM), storage (hard disk or solid-state drive), and other peripheral devices. Unlike virtual machines, physical machines are not emulated or abstracted and directly interact with the underlying physical hardware.

### Virtual Machine
- A virtual machine (VM) is a software implementation of a physical computer that executes programs like a real machine.
-  It allows multiple operating systems to run on a single physical computer by creating a virtual environment that acts as a separate computer. 
- Each virtual machine operates independently and has its own operating system, applications, and data, as well as its own virtual hardware, including network adapters, storage, and CPUs. 
- This enables multiple operating systems to run on a single physical machine, effectively isolating them from one another, and providing a layer of abstraction and isolation from the underlying hardware.
  
```
+-----------------------+
|    Physical Machine   |
+-----------------------+
|    Hypervisor Layer   |
+-----------------------+
| Virtual Machine 1     |
|   Operating System 1  |
|      Application 1    |
+-----------------------+
| Virtual Machine 2     |
|   Operating System 2  |
|      Application 2    |
+-----------------------+
|    ...                |
+-----------------------+

```

### Physical Server 

- A physical server is a standalone computer or computer system that is dedicated to running applications and services, such as web servers, database servers, or file servers.
-  Unlike virtual servers, which are software-based representations of a physical server, physical servers are actual physical computers, with all the associated hardware components, such as processors, memory, storage, and network interfaces.
- Physical servers are typically housed in data centers and are responsible for hosting critical applications and services for organizations. 
- They provide a reliable and secure platform for hosting these applications, as well as ensuring that they are available and accessible to users 24/7.

### Virtual Server 
- A virtual server is a server that is created and managed within a virtualization environment. It is a software-based representation of a physical server and functions as a standalone server, providing the same capabilities and services as a physical server.
-  Virtual servers are created and managed using virtualization software, such as VMware, Hyper-V, or VirtualBox, and can run on a physical server, which is known as the host machine.
-  Virtual servers are often used to provide a scalable and flexible solution for hosting applications and services, as they can be easily created, configured, and managed, without the need for physical hardware. 
-  They also provide a cost-effective alternative to physical servers, as multiple virtual servers can be created on a single physical machine, enabling organizations to maximize the utilization of their hardware resources.

### Does virtual server exist only in a virtual machine?
- A virtual server is created and run inside a virtual machine (VM). A virtual machine is a software-based representation of a physical computer that operates on an existing physical host machine.
-  The virtual machine provides an isolated environment in which a virtual server can run, providing the same functionality and capabilities as a physical server.
-  In a virtual environment, multiple virtual servers can run on a single physical host machine, allowing the efficient use of hardware resources and improved scalability. 
-  The virtual servers are isolated from one another, ensuring that a problem with one virtual server will not affect the others running on the same physical host.
-  In summary, virtual servers exist within virtual machines, and a virtual machine provides the isolated environment in which a virtual server operates.

### Can a single virtual machine have multiple virtual servers?
- Yes, a single virtual machine can have multiple virtual servers. This is one of the key benefits of virtualization technology. A virtual machine acts as a single computer system and can run multiple operating systems and applications, each in its own virtual environment. 
- This allows multiple virtual servers to be created and run on a single physical host machine, improving hardware utilization and providing the ability to allocate resources to individual virtual servers as needed.
- Each virtual server runs its own operating system and applications, providing complete isolation and independence from the others. 
- This makes it possible to run different applications and services on different virtual servers, or to run multiple instances of the same application for testing or load balancing purposes.
- In this way, virtualization enables organizations to achieve greater flexibility, scalability, and cost-effectiveness in their IT infrastructure.

### Can a physical machine run more than one server?
- Yes, a physical machine can run multiple servers, but it requires the use of virtualization technology. Virtualization allows multiple virtual servers to be created and run on a single physical host machine.
- Each virtual server operates in its own isolated environment and operates as if it were running on its own dedicated physical machine. 
- This means that each virtual server can have its own operating system, applications, and network configuration.
- Virtualization enables organizations to achieve greater utilization of their physical resources and to run multiple servers on a single machine, reducing hardware costs and increasing efficiency. 
- The virtual servers can be easily managed, scaled, and moved as needed, providing the flexibility and scalability that organizations require.
- In summary, while a physical machine can run multiple servers, it requires the use of virtualization technology to create and manage the virtual servers.

### Can a virtual machine has more than one os?
- Yes, a single virtual machine can run multiple operating systems. This is possible through a feature called "multi-booting," which allows a single physical machine to run multiple virtual machines, each with a different operating system. 
- This is particularly useful for testing, development, and deployment purposes, as it allows multiple operating systems to be run in isolation from one another, ensuring that any issues or changes made to one operating system do not impact the others.
  
### Summary of these concepts
- A virtual machine (VM) is a software simulation of a physical computer that provides a way to run multiple operating systems (OS) on a single physical machine. 
- A virtual machine acts as an isolated environment, which allows multiple operating systems to run on the same physical machine without interfering with each other. Each virtual machine can be allocated its own resources, such as memory, storage, and processing power, and can run its own operating system. 
- The physical machine runs a hypervisor, which creates and manages virtual machines, and allocates physical resources to each virtual machine as needed
- A virtual server is a virtual machine that runs a server operating system and serves the purpose of hosting and managing various applications, services, and data
- A virtual server can run multiple virtual machines and provide services to multiple clients over a network
- This allows for efficient use of physical resources and reduces the cost and complexity of maintaining multiple physical servers
- It is possible for a virtual machine to contain more than one OS, but this requires the use of a hypervisor that supports multi-OS installations
- Similarly, a single physical machine can run multiple virtual servers, providing the benefits of virtualization and allowing multiple applications, services, and data to be hosted and managed on a single physical machine

## Networks
- In computer networking, a **host** is a device that is connected to a network and has an IP address. For example, your laptop, smartphone, or tablet can be considered a host when connected to the Internet.
-  A host can serve as both a client and a server, depending on its role in the network. For example, your laptop can request data from a server (acting as a client) or serve data to other devices that request it (acting as a server).
- A **port** is a numerical label assigned to each endpoint of communication, used to identify a specific process to which the data is to be sent once it reaches the host machine. 
- For example, when you visit a website in your web browser, the browser sends a request to the server for the page you want to view. The request is sent to a specific port on the server, such as port 80 for HTTP or port 443 for HTTPS. The server then processes the request and sends back the requested data to the browser via the same port.
- In summary, ports are used to distinguish between different services and applications running on the same host and to route incoming data to the correct application or process. 
- In this example, the port helps the server distinguish between different incoming requests and route each request to the appropriate service or application for processing.
  
### Network Traffic/Protocols

**HTTP (Hypertext Transfer Protocol):**  
- This is a protocol used for transmitting data over the World Wide Web. HTTP is an application layer protocol that uses the Transmission Control Protocol (TCP) as its transport protocol.
-  HTTP is used to exchange text, images, and other content between a web server and a client (such as a web browser).
- **Use cases:** HTTP is used for any application that requires the transfer of text, images, and other content between a server and a client. For example, it is commonly used for websites, web services, and APIs.

**HTTPS (Hypertext Transfer Protocol Secure):** 
- This is a secure version of HTTP that uses SSL/TLS encryption to protect the data transmitted over the network.
-  HTTPS is used to provide secure communication over the internet and is commonly used for online banking, e-commerce transactions, and other applications that require data security.
- **Use cases:** HTTPS is used for any application that requires secure transmission of sensitive information, such as passwords, credit card numbers, and personal information. It is commonly used for online banking, e-commerce transactions, and other applications that require data security.

**TCP (Transmission Control Protocol):** 
- This is a reliable, connection-oriented protocol that ensures data is delivered between two endpoints without error. 
- TCP is a transport layer protocol that provides a reliable, ordered, and error-checked delivery of data packets between applications.
**Use cases:** TCP is used for any application that requires reliable, ordered, and error-checked delivery of data packets. It is commonly used for email, file transfers, and web browsing.

**UDP (User Datagram Protocol):** 
- This is an unreliable, connectionless protocol that does not guarantee delivery of data packets.
-  UDP is a transport layer protocol that is often used for real-time applications, such as voice and video streaming, where some data loss is acceptable.
- **Use cases:** UDP is used for any application that requires real-time delivery of data packets, where some data loss is acceptable. It is commonly used for video streaming, online gaming, and voice-over-IP (VoIP) applications.

Overall, the choice of protocol to use depends on the specific requirements of the application. HTTP and HTTPS are used for general web traffic, while TCP is used for reliable data transfer and UDP is used for real-time applications.





## Network File System (NFS)

- Network File System (NFS) is a distributed file system protocol that allows a computer on a network to access files over a network as if they were on its local hard drive.
-  NFS is commonly used in Unix and Linux environments, but it can also be used in Windows environments with the appropriate software.
-   NFS operates by having a server share one or more of its file systems, and clients mount the shared file systems on their local machines.
- Web servers are a common use case for NFS because they often need to share data and content across multiple machines. 
- **For instance**, a website may have a large number of images that need to be served to users. Instead of having one server handle all the requests for those images, the website could set up a cluster of servers, with each server handling a portion of the image requests. NFS could be used to share the images across all the servers in the cluster, so that each server can access the same content and serve it to users.
- By distributing the load across multiple machines, NFS helps to improve performance, reduce downtime, and make it easier to manage complex server configurations. 

## Application Servers, Sessions, Caches
### Sessions
**A server typically stores session details of a client in one of the following ways:**

- **Server-side sessions:** The session data is stored on the server in a file or a database, and a unique session ID is assigned to each client. The session ID is then sent to the client as a cookie, which is used to identify the session on subsequent requests. The server retrieves the session data using the session ID.

- **Client-side sessions**: In this approach, the session data is stored in a cookie on the client-side. The server sends the session data to the client as a cookie, and the cookie is sent back to the server on each subsequent request. This approach has some security concerns as the session data is stored on the client-side, and it can be tampered with.

- **Database sessions**: The session data is stored in a database, and a unique session ID is assigned to each client. The server retrieves the session data from the database using the session ID.

The choice of where to store session data depends on factors like the size of the session data, the number of clients, and the server's capabilities. However, server-side sessions are the most common approach used by servers to store session details of clients.

### Cache
- Servers use cache to improve performance and reduce load times for clients. When a client makes a request to a server, the server may have to perform time-consuming operations like accessing a database or processing data before sending a response. 
- Caching the result of such operations can significantly reduce the response time for subsequent requests.

**Servers can use several types of cache, including:**

- Content cache: This cache stores frequently accessed content such as images, videos, and HTML files, and serves them to clients without accessing the original source.

- **Database cache:** This cache stores frequently accessed database records in memory, reducing the number of disk accesses required to serve requests.

- **Application cache:** This cache stores frequently accessed application data or objects, improving application performance.

- CDN cache: Content Delivery Networks (CDNs) cache content at multiple locations around the world, reducing network latency and improving the performance of globally distributed websites.

- Cache can be stores in RAM, CPU Cache, Disk of the server instance.


  
`I give total credit to ChatGPT for these wonderful explanations`



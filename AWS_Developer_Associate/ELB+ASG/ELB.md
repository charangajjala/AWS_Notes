# Types of Load Balancers
- [Types of Load Balancers](#types-of-load-balancers)
  - [**Application Load Balancer (v2)**](#application-load-balancer-v2)
    - [ALB Hands on](#alb-hands-on)
  - [**Network Load Balancer**](#network-load-balancer)
  - [**Gateway Load Balancer**](#gateway-load-balancer)
  - [Sticky Sessions (Session Affinity)](#sticky-sessions-session-affinity)
  





## **Application Load Balancer (v2)**
- Application load balancers is Layer 7 (HTTP)
- Load balancing to multiple HTTP applications across machines 
(target groups)
- Load balancing to multiple applications on the same machine 
(ex: containers)
- Support for HTTP/2 and WebSocket
- Support redirects (from HTTP to HTTPS for example)
- Routing tables to different target groups:
   ![](Assets/2023-02-18-21-37-10.png)
  - Routing based on path in URL (example.com/users & example.com/posts)
  - Routing based on hostname in URL (one.example.com & other.example.com)
  - Routing based on Query String, Headers 
  (example.com/users?id=123&order=false)
- ALB are a great fit for micro services & container-based application 
(example: Docker & Amazon ECS)
- Has a port mapping feature to redirect to a dynamic port in ECS
- In comparison, we’d need multiple Classic Load Balancer per application
- **ALB - Target Groups**
   ![](Assets/2023-02-18-21-38-41.png)
  - EC2 instances (can be managed by an Auto Scaling Group) – HTTP 
  - ECS tasks (managed by ECS itself) – HTTP 
  - Lambda functions – HTTP request is translated into a JSON event
  - IP Addresses – must be private IPs
  - ALB can route to multiple target groups
  - Health checks are at the target group level
- Useful info
  - Fixed hostname (XXX.region.elb.amazonaws.com)
  - The application servers don’t see the IP of the client directly
  - The true IP of the client is inserted in the header X-Forwarded-For
  - We can also get Port (X-Forwarded-Port) and proto (X-Forwarded-Proto)
  - A Target Group in Amazon Web Services (AWS) can only contain instances or resources that are located within the **same region** as the Target Group.
  - This is because a Target Group is a **regional service** in AWS that is associated.
  - An **ALB or NLB** can only route traffic to resources that are located within the same region as the load balancer.

### ALB Hands on 
- Create two instances for creating a target group. Add User Data as well. Make sure to add security group that allows ssh and http traffic from any where. (like launch-wizard-1)
- Create a securtiy group that allows incming hhtp traffic from any where so could attach to load balancer
- Start creating load balancer, attach above sg 

  ![](Assets/2023-02-19-20-01-52.png)

- Add listener which defines target group to attach
  
  ![](Assets/2023-02-19-20-04-21.png)

- Now if can see our ec2 instances running in browser through both their individual hostnames(private DNS) and the common ALB hostname/DNS.
  
  ![](Assets/2023-02-19-20-09-56.png)

  ![](Assets/2023-02-19-20-10-59.png)

- We can observe, from alb dns we refresh , we get different hostnames because of load balancing

- To stop getting respone through instance dns, we can attach alb-sg to sg of these instances as source
  
   ![](Assets/2023-02-19-20-30-44.png)

- we can add rules to a listener of load balancer
  
  ![](Assets/2023-02-19-20-34-53.png)

  ![](Assets/2023-02-19-20-36-24.png)

## **Network Load Balancer**
  ![](Assets/2023-02-19-20-58-37.png)
- Network load balancers **(Layer 4)** allow to:
- Forward TCP & UDP traffic to your instances
- Handle millions of request per seconds
- Less latency ~100 ms (vs 400 ms for ALB)
- NLB has one static IP per AZ, and supports assigning Elastic IP
(helpful for whitelisting specific IP)
- NLB are used for extreme performance, TCP or UDP traffic
- Not included in the AWS free tier
- **Network Load Balancer –Target Groups**
  ![](Assets/2023-02-19-21-00-40.png)
  - EC2 instances
  - IP Addresses – must be private IPs
  - **Application Load Balancer**
  - Health Checks support the TCP, HTTP and HTTPS Protocols

## **Gateway Load Balancer**
![](Assets/2023-02-19-21-17-26.png)
- Deploy, scale, and manage a fleet of 3rd party network virtual appliances in AWS
- Example: Firewalls, Intrusion Detection and 
Prevention Systems, Deep Packet Inspection 
Systems, payload manipulation, …
- Operates at **Layer 3 (Network Layer)** – IP 
Packets
- Combines the following functions:
  - Transparent Network Gateway – single entry/exit for all traffic
  - Load Balancer – distributes traffic to your virtual appliances
- Uses the **GENEVE protocol on port 6081**

**Gateway Load Balancer –Target Groups**
- EC2 instances
- IP Addresses – must be private IPs
  
## Sticky Sessions (Session Affinity)
- It is possible to implement stickiness so that the 
same client is always redirected to the same 
instance behind a load balancer
- This works for Classic Load Balancers & 
Application Load Balancers
- The “cookie” used for stickiness has an 
expiration date you control
- Use case: make sure the user doesn’t lose his 
session data
- Enabling stickiness may bring imbalance to the 
load over the backend EC2 instances
- These cookies are set in the edit attributes of a target group
**Sticky Sessions – Cookie Names**
- Application-based Cookies
  - Custom cookie
    - Generated by the target
    - Can include any custom attributes required by the application
    - Cookie name must be specified individually for each target group 
    - Don’t use AWSALB, AWSALBAPP, or AWSALBTG (reserved for use by the ELB)
  - Application cookie
    - Generated by the load balancer
    - Cookie name is AWSALBAPP
- Duration-based Cookies
  - Cookie generated by the load balancer 
  - Cookie name is AWSALB for ALB, AWSELB for CLB


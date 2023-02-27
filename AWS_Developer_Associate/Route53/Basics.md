# Route53 Basics
- [Route53 Basics](#route53-basics)
  - [Domain Name System (DNS)](#domain-name-system-dns)
  - [Route53 Overview](#route53-overview)
  - [Records](#records)
  - [Hosted Zones](#hosted-zones)
  - [Route 53–Records TTL (Time To Live)](#route-53records-ttl-time-to-live)
  - [CNAME vs Alias](#cname-vs-alias)
  - [Alais Records](#alais-records)
  - [Route53 Hands-on](#route53-hands-on)

## Domain Name System (DNS)
Domain Name System which translates the human friendly hostnames 
into the machine IP addresses
- www.google.com => 172.217.18.36
- DNS is the backbone of the Internet
- DNS uses hierarchical naming structure
    - .com
      - example.com
        - api.example.com
        - www.example.com
        - 
**DNS Terminologies**
![](Assets/2023-02-25-21-11-10.png)
- Domain Registrar: Amazon Route 53, GoDaddy, …
- DNS Records: A, AAAA, CNAME, NS, …
- Zone File: contains DNS records
- Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
- Top Level Domain (TLD): .com, .us, .in, .gov, .org, …
- Second Level Domain (SLD): amazon.com, google.com, …

**How DNS Works**
![](Assets/2023-02-25-21-16-18.png)
- First, wen browser checks for fecthing IP of hostname in local dns server.
- If not found, asks to root dns server it reroutes to TLD name server, TLD reroutes to SLD name server.
- SLD name server is managed by **Domain Registrar: Amazon Route 53, GoDaddy,...**. This gives IP which will cached in Local dns server and given to client browser.

## Route53 Overview
![](Assets/2023-02-25-21-38-50.png)
- A highly available, scalable, fully 
managed and Authoritative DNS
  - Authoritative = the customer (you) 
  can update the DNS records 
- Route 53 is also a Domain Registrar
- Ability to check the health of your 
resources
- The only AWS service which 
provides 100% availability SLA
- Why Route 53? 53 is a reference to 
the traditional DNS port

## Records
How you want to route traffic for a domain
- Each record contains:
  - Domain/subdomain Name – e.g., example.com
  - Record Type – e.g., A or AAAA
  - Value – e.g., 12.34.56.78
  - Routing Policy – how Route 53 responds to queries
  - TTL – amount of time the record cached at DNS Resolvers
- Route 53 supports the following DNS record types:
  - (**must know**) A / AAAA / CNAME / NS
  - (advanced) CAA / DS / MX / NAPTR / PTR / SOA / TXT / SPF / SR
  - **A** – maps a hostname to IPv4
  - **AAAA** – maps a hostname to IPv6
  - **CNAME** – maps a hostname to another hostname
    - The target is a domain name which must have an A or AAAA record
    - Can’t create a CNAME record for the top node of a DNS namespace (Zone 
    Apex)
    - Example: you can’t create for example.com, but you can create for 
    www.example.com
  - **NS** – Name Servers for the Hosted Zone
    - Control how traffic is routed for a domain

## Hosted Zones
![](Assets/2023-02-25-21-43-21.png)
- A container for records that define how to route traffic to a domain and 
its subdomains
- **Public Hosted Zones** – contains records that specify how to route 
traffic on the Internet (public domain names)
application1.mypublicdomain.com
- **Private Hosted Zones** – contain records that specify how you route 
traffic within one or more VPCs (private domain names)
application1.company.internal
- You pay $0.50 per month per hosted zone

## Route 53–Records TTL (Time To Live)
![](Assets/2023-02-27-20-35-24.png)
- High TTL – e.g., 24 hr
  - Less traffic on Route 53
  - Possibly outdated records
- Low TTL – e.g., 60 sec.
  - More traffic on Route 53 ($$)
  - Records are outdated for less 
  time
  - Easy to change records
- Except for Alias records, TTL 
is mandatory for each DNS 
record

## CNAME vs Alias
- AWS Resources (Load Balancer, CloudFront...) expose an AWS hostname: 
 - lb1-1234.us-east-2.elb.amazonaws.com and you want myapp.mydomain.com
- CNAME:
  - Points a hostname to any other hostname. (app.mydomain.com => blabla.anything.com)
  - ONLY FOR NON ROOT DOMAIN (aka. something.mydomain.com) 
- Alias: 
  - Points a hostname to an AWS Resource (app.mydomain.com => blabla.amazonaws.com) 
  - Works for ROOT DOMAIN and NON ROOT DOMAIN (aka mydomain.com) 
  - Free of charge 
  - Native health check

## Alais Records
![](Assets/2023-02-27-20-51-59.png)
- Maps a hostname to an AWS resource
- An extension to DNS functionality
- **Automatically recognizes changes in the 
resource’s IP addresses**
- Unlike CNAME, it can be used for the **top node** 
of a DNS namespace (Zone Apex), e.g.: 
example.com
- Alias Record is always of type **A/AAAA** for 
AWS resources (IPv4 / IPv6)
- You can’t set the TTL

**Targets**
- Elastic Load Balancers
- CloudFront Distributions
- API Gateway
- Elastic Beanstalk environments
- S3 Websites
- VPC Interface Endpoints
- Global Accelerator accelerator
- Route 53 record in the same hosted zone
- You cannot set an ALIAS record for an **EC2 DNS name**






## Route53 Hands-on
- We can register a `domain_name` in aws but it costs 12/year
- After registering, we can create records with this domain, an A type record with "record_name" maps `record_name.domain_name.com` (sub domain) to an IPV4 Address.
- Create CNAME and Alais records to map to an ALB hostname and resource respectively.
- With CNAME , we cant map top level domain names (exampl.com) to another hostname but alias can map to resource
- We can use different routing policies on records to have control on different region level (ex latency policy). These records can be integrated with health checks to we can handle failovers of different regions.


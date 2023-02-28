# Solution architectures

## Typical 3 tier solution architecture
![](Assets/2023-02-28-22-30-52.png)

## LAMP Stack on EC2
- Linux: OS for EC2 instances
- Apache: Web Server that run on Linux (EC2)
- MySQL: database on RDS
- PHP: Application logic (running on EC2)
- Can add Redis / Memcached (ElastiCache) to include a caching tech
- To store local application data & software: EBS drive (root)

## WordPress on AWS 
![](Assets/2023-02-28-22-32-27.png)

- https://aws.amazon.com/blogs/architecture/wordpress-best-practices-on-aws/

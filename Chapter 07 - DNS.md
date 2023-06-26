# Section 1:
## DNS
- DNS is used to convert human-friendly domain names into an Internet Protocol addresses
- IP addresses are used by computers to identify each other on the network. IP addresses commonly come in 2 different forms: IPv4 and IPv6.
## IPv4 vs IPv6:
- IPv4 are running out
- IPv4 is 32-bit and has over 4 billion different addresses.
- IPv6 was created to solve this depletion issue and has an address space of 128 bits.
## Exam tip: Top-Level Domain
- If we look at common domain names, you will notice a string of characters separated by dots.
- The last word in a domain name represents the top-level domain.
- The second word in a domain name is known as a second-level domain name
## Top-Level Domains
- These top-level domain names are controlled by the Internet Assigned Numbers Authority(IANA) in a root zone database, which is essentially a database of all available top-level domains.
## Domain Registrars
- Because all names in a given domain name must be unique, there needs to be a way to organize this all so that domain names aren't duplicated.
- There is where domain registrars come in.
- A registrar is an authority that can assign domain names directly under one or more top-level domains. These domains are registered with InterNIC, a service of ICANN, which enforces uniqueness of domain names across the internet.
## Common DNS Record Types: SOA
- The SOA record stores information about:
  - The name of the server that supplied the data for the zone.
  - The administrator of the zone.
  - The current version of the data file.
  - The default number of seconds for the time-to-live file on resource records.
## NS stands for name server records
- NS records are used by top-level domain servers to direct traffic to the content DNS server that contains the authoritative DNS records.
## A Record:
- A(or address) record is the fundamental type of DNS record.
- The A record is used by a computer to translate the name of the domain to an IP address.
## TTL
- The length that a DNS record is cached on either the resolving server or the user's own local PC is equal to the value of the time to live(TTL) in seconds.
- The lower the time to live, the faster changes to DNS records take to propagate throughout the internet.
## CNAME
- Cname(canonical name) can be used to resolve one domain name to another. For example, you may have a mobile website with the domain name that is used for when users browse to your domain name on their mobile devices.
## Alias Records:
- Alias records are used to map resource record sets in your hosted zone to load balancers, CloudFront distributions or S3 buckets that are configured as websites.
- Alias records work like a CNAME record in that you can map one DNS name to another target DNS name.
## Route 53
- Route 53 is Amazon's DNS service.
- It allows you to register domain names, creat hosted zones and manage and create DNS records.
- There is 7 routing policies available with Route 53:
  - Simple Routing
  - Weighted Routing
  - Latency-Based Routing
  - Failover Routing
  - Geolocation Routing
  - Geoproximity Routing(Traffic Flow Only)
  - Multivalue Answer Routing
## Simple Routing Policy:
- If you choose the simple routing policy, you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route 53 returns all values to the user in a random order.
## Weighted Routing Policy:
- Allows you to split your traffic based on different weights assigned.
For example: You can set 10% of your traffic to go to us-east-1 and 90% to go to eu-west-1.
## Health Checks
- You can set Health Checkes on individual record sets.
- If a record set fails a health check, it will be removed from Route 53 until it passes the health check.
- You can set SNS notifications to alert you about failed health checks.
## Failover Routing Policy
- Failover routing policies are used when you want to create an active/passive set up.
## Geolocation Routing Policy
- Geolocation routing lets you choose where your traffic will be sent based on the geographic location of your users(i.e the location from which DNS queries originate).
- Use case: You might want all queries from Europe to be routed to a fleet of EC2 instances that are specifically configured for your European customers.
- Localization: These servers may have the local language of your European customers and display all prices in euros.
## Geoproximity Routing Policy
- Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources.
- You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias.
- Bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.
- To use geoproximity routing, you must use Route 53 traffic flow.
## Latency Routing Policy
- Allows you to route your traffic based on the lowest network latency for your end user(i.e which region will give them the fastest response time).
- To use latency-based routing, you create a latency resource record set for the EC2(or Elastic Load Balancer) resource in each region that hosts your website.
- When Route 53 receives a query for your site, it selects the latency resource record set for the region that gives the user the lowest latency.
- Route 53 then responds with the value associated with that resource record set.
## Multivalue Answer Routing
- Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries.
- You can specify multiple values for almost any record, but multivalue answer routing also lets you check the heath of each resource, so Route 53 returns only values for healthy resources.

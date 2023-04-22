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

# Section 1:
## VPC: Think of VPC as a virtual data center in the cloud.
- Logically isolated part of AWS Cloud where you can define your own network.
- Complete control of virtual network, including your own IP address range, subnets, route tables and network gateways.
## Network:
 - Fully Customizable Network: You can leverage multiple layers of security, including security groups and network access control lists:
    - Web: Public-facing subnet
    - Application: Private subnet. Can only speak to web tier and database tier.
    - Database: Private subnet. Can only speak to application tier.
## VPN:
- Additionally, you can create a hardware Virtual Private Network(VPN) connection between your corporate data center and you VPC and leverage the AWS Cloud as an extension of your corporate data center.
## VPC Features:
- Launch Instances: Launch instances into a subnet of your choosing. So we can launch them into private subnets or public subnets.
- Custom IP Addresses: Assign custom IP address ranges in each subnet.
- Route Tables: Configure route tables between subnets.
- Internet Gateway: Create internet gateway and attach it to our VPC.
- More Control: Much better security control over your AWS resources.
- Access Control Lists: Subnet network access control lists.
- You can use network access control lists(NACL) to block specific IP adresses.
## Default VPC vs Custom VPC:
### Default VPC:
- Default VPC is user friendly.
- All subnets in default VPC have a route out to the internet.
- Each EC2 instance has both a public and private IP address.
### Custom:
- Fully customizable.
- Takes time to setup.
## Exam tips:
- Think of a VPC as a logical data center in AWS.
- Consists of internet gateways (or virtual private gateways), route tables, network access control lists, subnets and security groups.
- 1 subnet is always in 1 Availability Zone.
# Section 2:
## NAT Gateways:
- You can use a network address translation(NAT) gateway to enable instances in a private subnet to connect to the internet or other AWS services while preventing the internet from initiating a connection with those instances.
- 5 Facts to remember about NAT Gateways:
  - Redundant inside the Availability Zone
  - Starts at 5 Gbps and scales currently to 45 Gbps.
  - No need to patch
  - Not associatiated with security groups.
  - Automatically assigned a public IP address.
# Section 3:
- Security Groups are virtual firewalls for an EC2 instance. By default, everything is blocked. To let everything in: 0.0.0.0/0
- In order to communicate to your EC2 instances via SSH, RDP or HTTP, you will need to open up the correct ports.
## Security Groups are stateful
- if you send a request from your instance, the response traffic for that request is allowed to flow in regardless of inbound security group rules.

# Section 4:
## Network ACLs: The first line of defense
- A network access control list(ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
- You might set up network ACLs with rules similar to your security groups in order to add another layer of security to your VPC.
  - Default Network ACLs: Your VPC automatically comes with a default network ACL, and by default it allows all outbound and inbound traffic.
  - Custom Network ACLs: You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound until you add rules.
  - Subnet Associations: Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.
  - Block IP Addresses: Block IP addresses using network ACLs, not security groups.
### Tips
- You can associate a network ACL with multiple subnets. However, a subnet can be associated with only 1 network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.
- Network ACLs contain a numbered list of rules that are evaluated in order, starting with the lowest numbered rule.
- Network ACLs have separate inbound and outbound rules, and each rule can either allow or deny traffic.
- Network ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic
# Section 5:
## VPC Endpoints:
- A VPC Endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection or AWS Direct Connect connection.
- Instances in your VPC do not require public IP addresses to communicate with resources in the service.
- Endpoints are virtual devices: They are horizontally scaled, redundant and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.
### VPC Endpoints Types: There are 2 types of endpoints:
- Interface Endpoints: An interface endpoint is an elastic network interface with a private IP address that serves as an entry point for traffic headed to a supported service. They support a large number of AWS services.
- Gateway Endpoints: Similar to NAT gateways, a gateway endpoint is a virtual device you provision. It supports connection to S3 and DynamoDB.
### Tips:
- Use case: When you want to connect AWS services without leaving the Amazon internal network.
- 2 types of VPC Endpoint: Interface endpoints and gateway endpoints.
- Gateway Endpoints: Support S3 and DynamoDB.
# Section 6:
## Multiple VPCs:
- Sometimes you may need to have several VPCs for different environments, and it may be necessary to connect these VPCs to each other.
- VPC Peering: Allow you to connect 1 VPC with another via a direct network route using private IP addresses.
- Instances behave as if they were on the same private network.
- You can peer VPCs with other AWS accounts as well as with other VPCs in the same account.
- Peering is in a star configuration(1 central VPC peers with 4 others). No transitive peering.
- You can peer between regions.
## Exam Tips:
- VPC Peering allow you to connect 1 VPC with another via a direct network route using private addresses.
- Transitive peering is not supported. This must always be in a hub-and-spoke model.
- You can peer between regions.
- No overlapping CIDR address ranges.
# Section 7:
- Open the VPC up to the internet:
  - Security considerations everything in the public subnet is public.
  - A lot more to manage
- Use VPC Peering:
  - You will have to create and manage many different peering relationships.
  - The whole network will be accessible. This isn't good if you have multiple applications within your VPC.
## Using PrivateLink:
- The best way to expose a service VPC to tens, hundreds or thousands of customer VPCs.
- Doesn't require VPC peering; no route tables, NAT gateways, internet gateways, etc.
- Requires a Network Load Balancer on the service VPC and an ENI on the customer VPC.
## Exam tips:
- If you see a question asking about peering VPCs to tens, hundreds or thousands of customer VPCs. Think of AWS PrivateLink.
- Doesn't require VPC peering; no route tables, NAT gateways, internet gateways, etc.
- Require a Network Load Balancer on the service VPC and an ENI on the customer VPC.
# Section 8:
- VPN CloudHub: If you have multiple sites, each with its own VPC connection, you can use AWS VPN CloudHub to connect those sites together.
- Hub-and-spoke model.
- Low cost and easy to manage.
- It operates over the public internet, but all traffic between the customer gateway and the AWS VPN CloudHub is encrypted.
# Section 9:
## Direct Connect:
- AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premise to AWS.
- Private connectivity: Using AWS Direct Connect, you can establish private connectivity between AWS and your data center or office.
- In many cases, you can reduce your network costs, increase bandwidth throughput and provide a more consistent network experience than internet-based connections.
## 2 types of Direct Connect Connection:
- Dedicated Connection: A physical Ethernet connection associated with a single customer. Customers can request a dedicated connection through the AWS Direct Connect console, the CLI or the API.
- Hosted Connection: A physical Ethernet connection that an AWS Direct Connect Partner provisions on behalf of a customer. Customers request a hosted connection by contacting a partner in the AWS Direct Connect Partner Program, who provisions the connection.
## VPNs vs Direct Connect:
- VPNs allow private communication, but it still traverses the public internet to get the data delivered. While secure, it can be painfully slow.
- Direct Connect is:
  - Fast
  - Secure
  - Reliable
  - Able to take massive throughput.
## Exam tips:
- Direct Connect directly connects your data center to AWS.
- Useful for high-throughput workloads
- Helpful when you need a stable and reliable secure connection.

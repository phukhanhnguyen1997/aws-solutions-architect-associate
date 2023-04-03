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

# EC2
- EC2 is one of the most fundamental.
- Elastic Compute Cloud
- It’s virtual machine and is hosted in AWS.
- Design to make web-scale cloud computing easier for developers.
- The capacity you want when you need it
- You are in complete control of your own instances.
- Only pay for what you use
- No wasted capacity.
- On-prsemises infrastructure:
  - Estimate Capacity: long-term investment, 3-5 years. Expectation that the application will “grow into” it.
  - Wait minutes, not months. All you needed was to basically provide credit card details. After that it would be done throught software, but basically via an API call, and it would provision our EC2 instances in minutes.
- Ec2 Pricing Options:
  - On-demand: Pay by hour or second, depending on the type of instance you run.
  - Reserved Capacity: You get into a contract with AWS for between 1-3 years. The longer the contract and the more you pay upfront, the greater discount you get. If you want to save the most amount of money, if you want to save money compared to On-Demand, what you do is you reserve capacity. Up to 72% discount on the hourly charge.
  - Spot: Purchase unused capacity at a discount up to 90%, but prices flutuate with supply and demand.
  - Dedicated: A physical EC2 server dedicated for your use. This is the most expensive option.
- On-Demand Instances: test or dev
  - Flexible: Low cost and flexibility of Amazon EC2 without any upfront payment or long-term commitment.
  - Short-term: Applications with short-term, spiky or unpredictable workloads that cannot be interrupted.
  - Testing the Water: Applications being developed or tested on Amazon EC2 for the first time.
- Reserved Instances: operate at a regional level
  - Predictable Usage: Applications with steady state or predictable usage.
  - Specific Capacity Requirements: Applications that require reserved capacity.
  - Pay up font: You can make upfront payments to reduce the total computing costs even further.
  - Standard RIs: Up to 72% off the on-demand price.
  - Convertible RIs: Up to 54% off the on-demand price. Has the option to change to a different RI type of equal or greater value.
  - Scheduled Reserved Instances: Launch within the time window you define. Match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, week or month.
- Spot Instances:
  - Applications that have flexible sgtart and end times.
  - Applications that are only feasible at very low compute prices.
  - Users with an urgent need for large amounts of additional computing capacity.
- Dedicated Hosts:
  - Compliance: Regulatory requirements that may not support multi-tenant virtualization.
  - Licensing: Great for licensing that does not support multi-tenancy or cloud deployments.
  - On-Demand: Can be purchased on-demand(hourly).
  - Reserved: Can be purchased as a reservation for up to 70% off the on-demand price.
? Exam tips: 
EC2 like virtual machine. 
Select the capacity you need right now.
Grow and shrink when you need.
Pay for what you use.
Wait minutes, not months.
Any question talks about special licensing requirements -> Dedicated Hosts. Dedicated host is physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts allow you to use your existing per-socket, per-core, per-VM software licenses, including Windows Server, Microsoft SQL Server, and SUSE Linux Enterprise Server
AWS CLI exam tips:
Always give your users the minimum account of access required to do their job.
Create IAM groups and assign your users to those groups. Group permissions are assigned using IAM policy documents.
Secret Access Key: You will only see it once. If you lose it, you can delete and regenerate them. You will need to run aws config again.
Don’t share your key pairs: Each developer should have their own access key ID and secret access key. Just like password, they should not be shared.
CLI are supported in Linux, Windows and MacOS.
AWS Roles Tips:
Roles is preferred option from a security perspective.
Avoid hard-coding your credentials
Policies control a role’s permissions.
You can update a policy attached to a role and it will take immediately effect.
You can attach and detach roles to running ec2 instances without having to stop or terminate those instances.
Security groups is virtual firewalls for EC2 instances. By default, everything is blocked.
To let everything in: 0.0.0.0/0
In order to be able to communicate to your EC2 instances via SSH/RDP/HTTP, you will need to open up the correct ports.
Bootstrap Scripts is a scripts that runs when the instances first runs. 
AWS Security Groups Tips:
Change to security groups take effect immediately.
You can have any number of EC2 instances within a security group.
You can have multiple security groups attached to EC2 instances.
All inbound traffic is blocked by default.
All outbound traffic is allowed.
EC2 metadata is simply data about our EC2 instances. This include private IP address, public IP address, hostname, security groups
AWS Metadata Tips:
User data is simply bootstrap scripts.
Metadata is data about our EC2 instances.
You can use bootstrap scripts to access metadata.
Different Virtual Networking Options: You can attach 3 different types of virtual networking cards to your EC2 instances
ENI: Elastic Network Interface, for basic, day-to-day networking
EN: Enhanced Networking: Uses single root I/O virtualization(SR-IOV) to provide high performance.
EFA: Elastic Fabric Adapter: Accelerates High Performance Computing(HPC) and machine learning applications.
Elastic Network Interface(ENI) is simply a virtual network card that allows:
Private IPv4 Addresses
Public IPv4 Addresses
Many IPv6 Addresses
MAC Address
1 or More Security Groups
Use case:
Create a management network
Use network and security appliances in your VPC
Create dual-homed instances with workloads/roles on distinct subnets.
Create a low-budget, high-availability solution.
Enhaned Networking for high performance:
Single Root I/O virtualization provides higher I/O performance and lower CPU utilization.
Provides higher bandwidth, higher packet per second(PPS) performance, and consistently lower inter-instance latencies.
Depending on your instance type, enhanced networking can be enabled using:
Elastic Network Adapter(ENA): Supports network speeds of up to 100 Gbps for supported instance types
Intel 82599 Virtual Function(VF) Interface: Supports network speeds of up to 10Gbps for supported instance types. Typically used on older instances.
=> choose ENA over VF interface in any scenario question.
Elastic Fabric Adapter(EFA):
A network device you can attach to your Amazon EC2 instance to accelerate High Performance Computing(HPO) and machine learning applications.
Provides lower and more consistent latency and higher throughput than the TCP transport tradtitionally used in cloud-based HPC systems.
For different scenarios, choose the correct networking device:
ENI: For basic networking. Perhaps you need a separate management networking from your production network or a separate logging network, you need to do this at a low cost. In this scenario, use multiple ENIs for each network.
Enhanced Networking: When you need speeds between 10 Ggbps and 100Ggbps. Anywhere you need reliable, high throughput.
EFA: You need to accelerate High Performance Computing and maching learning applications or if you need to do an OS-bypass. If you see a scenario question mentioning HPC or ML and asking what network adapter you want, choose EFA.
Cluster Placement Groups: Grouping of instances within a single Availability Zone. Recommended fỏ applications that need low network latency, high network throughput or both.
Spread Placement Groups: A spread placement group is a group of instances that are each placed on distinct underlying hardware. Recommended for applications that have a small number of critical instances that should be kept separate from each other.
Partition Placement Groups: Each partition placement group has its own set of racks. Each rack has its own network and power source. No two partitions within a placement group share the same racks, allowing you to isolate the impact of hardware failure within your application.
Exam tips:
Cluster placement group can’t span multiple Availability Zones, whereas a spread placement group and partition placement group can.
Only certain types of instances can be launched in a placement group(compute optimized, GPU, memory optimized, storage optimized)
AWS recommends homogenous instances within cluster placement groups.
You can’t merge placement groups.
You can move an existing instances into a placement group. Before you move the instance, the instance must be in the stopped state. You can move or remove an instance using the AWS CLI or an AWS SDK, but you can’t do it via the console yet.
Spot Instances:
You need stateless, fault tolerant or flexible applications. So you wouldn’t use with things like web servers because it run on all the time. 
Applications such as bug data, containerized workloads, CI/CD, high-performance computing, and other test and development workloads.
First, you must decide your maximum Spot price. The instance will be provisioned so long as the sport price is BELOW your maximum Spot price.
If the Spot price goes above your maximum, you have 2 minutes to choose whether to stop or terminate your instance.
You can also use Spot Block to stop your Spot Instances from being terminated even if the Spot price goes over your max Spot price. You can set Spot blocks for between 1 to 6 hours currently.
Spot Instances are not useful for
Persistent workloads: web server
Critical job(you don’t want your Spot Instances to be stopped)
Databases
(?) How do you go in and terminate Spot Instances under a persistent spot request? => You just go in and you cancel the spot requests and you go in and you terminate your instances
Spot fleets is a collection of SPot Instances and (optionally) on-Demand Instances.
The spot Fleet attempts to launch the number of Spot Instances and on-Demand instances to meet the target capacity you specified in the Spot Fleet request. The request for Spot Instances is fulfilled if there is available capacity and the maximum price you specified in the request exceeds the current Spot price. The Spot Fleet also attempts to maintain its target capacity fleet if your Spot Instances are interrupt.
capacityOptimized: The Spot Instances come from the pool with optimal capacity for the number of instances launching.
lowestPrice: The Spot Instances come from the pool with the lowest price. This is the default strategy.
diversified: The Spot Instances are distributed across all pools.
InstancePoolsToUseCount: The Spot Instances are distributed across the number of Spot Instance pools you specify. This parameter is valid only when used in combination with lowestPrice.
Exam tips: 
Spot Instances saved up 90% of the cost of On-Demand Instances.
Useful for any type of computing where you don’t need persistent storage.
You can block Spot Instances from terminating by using a Spot block.
A Spot Fleet is a collection of Spot Instances and (optionally) On-Demand Instances.
VMware is used by organizations around the world for private cloud deployments. Some organizations opt for a hybrid cloud strategy and would like to leverage AWS services.
Use cases for VMware:
Hybrid Cloud: Connect your on-premises cloud to the AWS public cloud, and manage a hybrid workload.
Cloud Migration: Migrate your existing cloud environment to AWS using VMware’s build-in tools.
Disaster Recovery: VMware is famous for its disaster recovery technology. Using hybrid cloud, you can have an inexpensive disaster recovery environment on AWS.
Leverage AWS: Use over 200 AWS services to update your applications or to create new ones.
VMware runs on dedicated hardware hosted in AWS using a single AWS account.
Each host has two sockets with 18 cores per socket, 512 GiB Ram, and 15.2 TB Raw SSD storage.
Each host is capable of running multiple VMware instances(up to the hundreds)
Clusters can start with two hosts up to a maximum of 16 hosts per cluster.
Exam tips:
You can deploy vCenter on the AWS cloud using VMware.
Perfect solution for extending your private VMware Cloud into the AWS public cloud.
Outposts brings the AWS data center directly to you, on-premises. Outposts allows you to have the large variety of AWS services in your data center. You can have Outposts in sizes such as 1U and 2U servers all the way up to 42U racks and multiple-rack deployments.
Benefits of Outposts:
Hybrid Cloud: Create a hybrid cloud where you can leverage AWS services inside your own data center.
Fully Managed Infrastructure: AWS can manage the infrastructure for you. You do not need a dedicated team to look after your Outposts infrastructure.
Consistency: Bring the AWS Management Console, APIs, and SDK into your data center, allowing uniform consistency in your hybrid environment.
Outposts family members:
Outposts Rack:
Hardware: Available starting with a single 42U rack and scale up to 96 racks.
Services: Provides AWS compute, storage, database and other services locally.
Results: Gives the same AWS infrastructure, services and APIs in your own data center.
Outposts Servers:
Individual servers in 1U or 2U form factor.
Use cases: Useful for small space requirements, such as retail stores, branch offices, healthcare provider locations or factory floors.
Results: Provides local compute and networking services.
Process: 
1/ Order: Log in to AWS console and order your Outposts configuration.
2/ Install AWS staff will come on-site to install and deploy the hardware, including power, networking and connectivity.
3/ Launch: Using the AWS Management Console, you can launch instances on your Outpost on-site.
4/ Build: Start building your on-site AWS environment.
Exam tips:
Extending AWS into your data center -> AWS Outposts.
AWS Outpots Rack for large deployment, within a data center.
AWS Outposts Servers for smaller deployments such as retail environments, shop…
EC2 Exam Tips:
EC2 is like an VM, hosted in AWS instead of your own data center.
Select the capacity you need right now. Grow and shrink when you need.
Pay for what you use.
Wait minutes, not months.
On-Demand: Pay for the hour or the second, depending on the type of instance you run. Great for flexibility.
Spot: Purchase unused capacity at a discount of up to 90%. Prices fluctuate with supply and demand. Great for applications with flexible start and end times.
Reserved Instances: Reserved capacity for 1 or 3 years. Up to 72% discount on the hourly charge. Great if you have known, fixed requirements.
Dedicated: A physical EC2 server dedicated for your use. Great if you have server-bound licenses to reuse or compliance requirements.
AWS Command Line Interface:
Least Privilege: Always give your users the minimum amount of access required to do their job.
Use Groups: Create IAM groups and assign your users to groups. Group permissions are assigned using IAM policy documents. Your users will automatically inherit the permissions of the groups.
Secret Access Key: You will only see this once. If you lose it, you can delete the access ID and secret access key and regenerate them. You will need to run `aws configure` again.
Don’t share your key pairs: Each developer should have their own access key ID and secret access key. Just like password, they should not be shared.
Support Linux, Windows and MacOS
Using Roles:
The preferred Option: Roles are preferred from a security perspective.
Avoid hard coding your credentials: Roles allow you to provide access without the use of access key IDs and secret access keys.
Policies: Policies control a role’s permission.
Updates: You can update a policy attached to a role, and it will take immediately effect.
Attach and detach: You can attach and detach roles to running EC2 instances without having to stop or terminate these instances.
Security Groups:
Changes to security groups take effect immediately
You can have any number of EC2 instances within a security group.
You can have multiple security groups attached to EC2 instances.
All inbound traffic is blocked by default.
All outbound traffic is allowed.
Bootstrap Scripts runs on the first run.
User data: simply bootstrap scripts.
Metadata is data about your EC2 instances. You can use bootstrap scripts to access metadata
Networking device:
ENI: basic networking, need to separate management networking from your production network at a low cost -> multiple ENIs for each network
Enhanced Networking: Between 10 Gbps and 100 Gbps. Anywhere you need reliable, high throughput.
EFA: High Performance Computing and machine learning or if you need to do an OS-bypass.
3 types of placement groups
Cluster Placement Groups: Low network latency, high network throughput
Spread Placement Groups: Individual critical EC2 instances
Partition Placement Groups: Multiple EC2 instances, HDFS, Hbase, Cassandra
A cluster placement group can’t span multiuple Availability Zones, whereas a spread placement group and partition placement group can.
Only certain types of instances can be launched in a placement group(compute optimized, GPU, memory optimized, storage optimized)
AWS recommend homogenous instances within cluster placement groups.
You can’t merge placement groups.
You can move an existing instance into a placement group. Before move the instance, the instance must be in the stopped state. You can move or remove an instance using the AWS CLI or AWS SDK, but you can’t do it via the console yet.
Any question talks about special licensing requirements -> dedicated hosts
Spot instances and Spot Fleet Tips:
Spot Instances save up to 90% of the cost of On-Demand instances.
Useful for any type of computing where you don’t need persistent storage.
You can block Spot Instances from terminating by using Spot block.
A Spot Fleet is a collection of Spot Instances and optionally On-demand Instances.
Spot Instances with a defined duration(Spot blocks) no longer supported.
You can deploy vCenter on the AWS cloud using VMware. Perfect solution for extending your private VMware Cloud into the AWS public cloud.(cloud migration or just basically doing disaster recovery using AWS but you want all native tools that come with VMware and within vCenter itself)
Question about extending AWS to your data center -> AWS Outposts.
AWS Outpost racks: large deployments 42U form factor racks
AWS Outpost servers: small deployments, this will be things like putting in a 1U server inside a retail shop.

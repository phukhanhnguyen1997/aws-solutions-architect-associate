EBS
EBS stands for Elastic Block Storage. phukhanh1997
There are different type of EBS volumns available.
There’s different use case for each type.
Storage volumn that you can attach to your EC2 instances.
EBS give us an ability to install all kind of data. It’s basically just a virtual hard disk that is attached to your virtual EC2 instances.
Use it the same way you would use any system disk
Create a file system
Run a database
Run an operating system
Storage data
Install applications.
Mission Critical:
Production workloads: Designed for mission-critical workloads.
Highly Available: Automatically replicated within a single Availability Zone to protect against hardware failures.
Scalable: Dynamically increase capacity and change the volumn type with no downtime or performance impact to your live systems.
Solid State Disk(SSD):
General purpose SSD(gp2): a balance of price and performance. Good for boot volumnes or development and test applications that are not latency sensitive
General purpose SSD(gp3): Ideal for applications that require high performance at a low cost, such as MySQL, Cassandra, virtual desktop and Hadoop analytics.
gp, gp2 or gp3 just using that to install an operating system on. It’s basically the default volume that you would use when you provision an EC2 instance.
io1: high-performance option and the most expensive. Designed for I/O intensive applications, large databases and latency-sensitive workloads.
io2: latest generation, higher durability and more IOPS. io2 is the same price as io1.
Hard Disk Drive:
st1: 
low-cost HDD volume. 
Frequently accessed, throughput-intensive workloads. 
Big data, data warehouse, ETL and log processing => throughput
A cost-effective way to store mountains of data
Cannot be a boot volume
cold hdd(sc1):
lowest cost option
a good choice for colder data requiring fewer scans per day
good for applications that need the lowest cost and performance is not a factor.
cannot be a boot volume
IOPS vs Throughput
IOPS:
Measure the number of read and write operations per second
Important metric for quick transactions, low-latency apps, transactional workloads.
The ability to action reads and writes very quickly
Choose Provisioned IOPS SSD(io1 or io2)
Throughput:
Measure the number of bits read or written per second.
Important metric for large datasets, large I/O sizes, complex queries.
The ability to deal with large datasets.
Choose throughput optimized HDD(st1)
Exam tips: 
gp2: 
suitable for boot disks and general applications
up to 16k iops per volume
gp3: 
suitable for high performance applications
preditable 3000 iops baseline performance and 125 MiB/s regardless of volume size
up to 99.9% durability
Provisioned IOPS SSD(io1)
suitable for OLTP(online transaction processing) and latency-sensitive applications
50 IOPS/GiB
Up to 64k IOPS per volume
high performance and most expensive
up to 99.9% durability
Provisioned IOPS SSD
suitable for OLTP and latency-sensitive
500 IOPS/GiB
64k IOPS/volume
99.999% durability
Latest generation of Provision IOPS SSD
=> If you want more than 16k IOPS -> move from general purpose ssd to I/O intensive.
st1:
throughput optimized hdd
suitable for big data, data warehouses and etl
max throughput is 500 MB/s per volume
Cannot be a boot volume
up to 99.9% durability
sc1:
max throughput of 250 MB/s per volume
Less frequently accessed data
Cannot be a boot volume
lowest cost
What are volumes?
Volumes exist on EBS. It’s simply virtual hard disks. You need a minimum of 1 volume per EC2 instance. This is called the root device volume.
What are snapshot?
Snapshot exist on S3. It’s not exist on EBS: Think of snapshot as a photograph of the virtual disk/volume.
Snapshots are point in time: When you take a snapshot, it is a point-in-time copy of a volume.
Snapshots are incremental: This means only the data that has been changed since your last snapshot are moved to S3. This saves dramatically on space and the time it takes to take a snapshot.
The first snapshot: If it is your first snapshot, it may take some time to create as there is no previous point-in-time copy.
3 tips:
Consistency snapshots: Snapshot only capture data that has been written to your Amazon EBS volume, which might exclude any data that has been locally cached by your application or OS. For a consistency snapshot, it is recommended you stop the instance and take a snap.
Encrypted Snapshots: If you take a snapshot of an encrypted EBS volume, the snapshot will be encrypted automatically.
Sharing Snapshots: You can share snapshots but only in the region in which they were created. To share to other regions, you will need to copy them to the destination region first.
EBS volumes:
Location: EBS volumes will always be in the same AZ as EC2. Your EBS volumes will always be the same AZ as the EC2 instance to which it is attached
Resizing: Resize on the fly. You can resize EBS volumes on the fly. You do not need to stop or restart the instance. However, you will need to extend the filesystem in the OS so the OS can see the resized volume.
Volume type: Switch volume types. You can change volume types on the fly (eg from gp2 to io2). You do not need to stop or restart the instance.
Exam tips:
Volume exist on EBS, whereas snapshots exist on S3.
Snapshot are point-in-time photographs of volumes and are incremental in nature.
The first snapshot will take sometime to create. For consistent snapshots, stop the instance and detach the volume.
You can share snapshots between AWS accounts as well as between regions, but first you need to copy that snapshot to the target region.
You can resize EBS volumes on the fly as well as changing the volume types.
EBS Encryption:
EBS encrypts your volume with a data key using the industry-standard AES-256 algorithm. Amacon EBS encryption uses AWS Key Management Service(AWS KMS) customer master keys(CMK) when creating encrypted volumes and snapshots.
When you encrypt an EBS volume:
Data at rest is encrypted inside the volume.
All data in flight moving between the instance and the volume is encrypted.
All snapshots are encrypted.
All volumes created from the snapshot are encrypted.
EBS Encryption:
Handled Transparently: Encryption and decryption are handled transparently(you don’t need to do anything).
Latency: Encryption has a minimal impact on latency.
Copying: Copying an unencrypted snapshots allows encryption.
Snapshots: Snapshots of encrypted volumes are encrypted.
Root device volume: You can now encrypt root device volumes upon creation.
4 steps to encrypt an unencrypted volume:
Create a snapshot of the unencrypted root device volume.
Create a copy of the snapshot and select the encrypt option
Create an AMI from the encrypted snapshot.
Use the AMI to launch new encrypted instance.
Exam tips:
Data at rest is encrypted inside the volume.
All data in flight moving between the instance and the volume is encrypted.
All snapshots are encrypted.
All volumes created from the snapshot are encrypted.
EBS Behavior Reviewed:
We have learned so far we can stop and terminate EC2 instances. If we stop the instance, the data is kept on the disk(with EBS), and will remain on the disk until the EC2 instance is started. If the instance is terminated, then by default the root device volume will also be terminated.
When we start our EC2 instance, the following happens:
Operating system boots up.
User data script is run(bootstrap scripts)
Applications start(can take some time)
EC2 Hibernation:
When you hibernate an EC2 instance, the operating system is told to perform hibernation(suspend-to-disk). Hibernation saves the contents from the instance memory(RAM) to your Amazon EBS root volume. We persist the instance’s Amazon EBS root volume and any attached Amazon EBS data volumes.
When you start your instance out of hibernation:
The Amazon EBS root volume is restored to its previous state.
The RAM contents are reloaded.
The processes that were previously running on the instance are resumed.
Previously attached data volumes are reattached and the instance retains its instance ID.
With EC2 Hibernation, the instance boots much faster. The operating system does not need to reboot because the in-memory state(RAM) is preserved. This is useful for:
Long-running processes
Services that take time to initialize
What you need to know about EC2 Hibernation:
EC2 hibernation preserves the in-memory RAM on persisten storage(EBS).
Much faster to boot up because you do not need to reload the operating system.
Instance RAM must be less than 150GB.
Instance familities include C3, C4, C5, M3, M4, M5, R3, R4 and R5.
Available for Windows, Amazon Linux 2 AMI and Ubuntu.
Instances can’t be hibernated for more than 60 days.
Available for On-Demand instances and Reserved Instances.
EFS: Elastic File System
Managed NFS(network file system) that can be mounted on many EC2 instances.
EFS works with EC2 instances in multiple Availability Zones.
Highly available and scalable, however, it is expensive.
Use cases:
Content Management: Great fit for content management systems, as you can easily share content between EC2 instances.
Web servers: Also great fit for web servers. Have just a single folder structure for your website.
Overview:
Use NFSv4 protocol
Compatible with Linux-based AMI(windows not supported at this time).
Encryption at rest using KMS.
File system scales automatically, no capacity planning required.
Pay per use.
EFS performance: Amazing performance capabilities:
1000s concurrent connections: can support thousands of EC2 instances.
10 Gbps Throughput
Scale your storage to petabytes
Controlling performance: When creating and EFS file system, you can set what performance characteristics you want
General Purpose: Used for things like web servers, CMS, etc…
Max I/O: Use for big data, media processing, etc…
Storage Tiers: EFS comes with storage tiers and lifecycle management, allowing you to move your data from one tier to another after X number of days.
Standard: For frequently accessed files
Infrequently Accessed: For files not frequently accessed.
Exam tips:
Support the Network File System version 4(NFSv4) protocol
Only pay for the storage you use(no pre-provisioning required)
Can scale up to petabytes.
Can support thousands of concurrent NFS connections.
Data is stored across multiple AZs within a region.
Read-after-write consistent.
If we have a scenario-based question around highly scalable shared storage using NFS, think EFS.
FSx: Amazon FSx is built on Windows server.
Amazon FSx for Windows File Server provides a fully managed native Microsoft Windows file system so you can easily move your Windows-based applications that require file storage to AWS.
FSX for windows:
A managed Windows Server that runs Windows Server Message Block(SMB)-based file services.
Designed for Windows and Windows applications.
Supports AD users, access control lists, groups, and security policies, along with Distributed File System(DFS) namespaces and replication.
EFS:
A managed NAS filer for EC2 instances based on Network File System(NFS) version 4.
One of the first network file sharing protocols native on Unix and Linux.
Amazon FSx for Lustre: A fully managed file system that is optimized for compute-intensive workloads
High Performance Computing
Machine Learning
Media Data Processing Workflows
Electronic Design Automation
FSx for Lustre Performance: With Amazon FSx, you can launch and run a Lustre file system that can process massive datasets at up to hundreds of gigabytes per second of throguhput, millions of IOPS and sub-milisecond latencies.
Exam tips:
EFS: When you need distributed, highly resilient storage for Linux instances and Linux-based applications.
Amazon FSx for Windows: When you need centralized storage for Windows-based applications, such as SharePoint, Microsoft SQL Server, Workspace, IIS Web Server or any other natiev Microsoft application.
Amazon FSx for Lustre: When you need high-speed, high-capacity distributed storage. This will be for applications that do high performance computing(HPC), financial modeling, etc… Remember that FSx for Lustre can store data directly on S3.
AMI: Amazon Machine Image
An AMI provides the information required to launch an instance.
You must specify an AMI when you launch an instance.
5 things you can base your AMI on:
Region
Operating System
Architecture(32-bit or 64-bit)
Launch permissions
Storage for the root device(root device volume)
All AMI are categorized as either backed by:
Amazon EBS: The root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot.
Instance Store: The root device for an instance launched from the AMI is an instance stored volume created from a template stored in Amazon S3.
Instance Store Volume are sometimes called ephemeral storage. Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data. You can, however, reboot the instance without losing your data.
If you. delete the instance, you will lose the instance store volume.
EBS volumes:
EBS-backed instances can be stopped. You will not lose the data on this if it is stopped. You can also reboot an EBS volume and not lose your data.
By default, the root device volume will be deleted on termination. However, you can tell AWS to keep the root device volume with EBS volumes.
EBS vs Instance Store:
Instance store volumes are sometimes called ephemeral storage.
Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data.
EBS-backed instances can be stopped. You will not lose the data on this instance if it is stopped.
You can reboot both EBS and instance store volumes and you will not lose your data.
By default, both root volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume.
An AMI is just a blueprint for an EC2 instance.
AWS Backup: 
Backup allows you to consolidate your backups across multiple AWS services, such as EC2, EBS, FPS, Amazon FSx for Lustre, Amazon FSx for Windows File Server, and AWS Storage Gateway.
It can include other services, such as database technologies like RDS and DynamoDB.
AWS Backup with Organizations: Backup can be used with AWS Organizations to back up multiple AWS accounts in your organization. It gives you centralized control across all AWS services, in multiple AWS accounts across the entire AWS organization.
Benefits:
Central Management: Use a single, central backup console, allowing you to centralize your backups across multiple AWS serivces and multiple AWS accounts.
Automation: You can create automated backup schedules and retention policies. You can also create lifecycle policies, allowing you to expire unnecessary backups after a period of time.
Improved Compliance: Backup policies can be enforced while backups can be encrypted both at rest and in transit, allowing alignment to regulatory compliance. Auditing is made easy due to a consolidated view of backups across many AWS services.
Exam tips:
Consolidation: Use AWS Backup to backup AWS services, such as EC2, EBS, EFS, Amazon FSx for Lustre, Amazon FSx for Windows File Server and AWS Storage Gateway.
Organizations: You can use AWS Organizations in conjunction with AWS backup to backup your different AWS services across multiple AWS accounts.
Benefits: Backup gives you centralized control, letting you automate your backups and define lifecycle policies for your data. You get better compliance, as you can enfore your backups policies, ensure your backups are encrypted and audit them once complete.
EBS Exam Tips:
EBS: SSD Volumes
gp2
gp3
io1
io2
EBS: HDD Volumes:
st1: Cannot be a boot volume
sc1: Cannot be a boot volume, lowest cost
5 tips for EBS Volumes and Snapshots:
Volumes exist on EBS, whereas snapshots exist on S3.
Snapshots are point-in-time photographs of volumes and are incremental in nature.
The first snapshot will take some time to create. For consistent snapshots, stop the instance and detach the volume.
You can share snapshots between AWS accounts as well as between regions, but first you need to copy that snapshot to the target region.
You can resize EBS volumes on the fly as well as changing the volume types
AMI: EBS vs Instance Store:
Instance store volumes are sometimes called ephemeral storage.
Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data.
You can reboot both EBS and instance store volumes and you will not lose your data.
By default, both root volumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume.
EBS-backed instances can be stopped. You will not lose the data on this instace if it is stopped.
AMI is just a blueprint for an EC2 instance.
Exam tips:
Encrypted volumes:
Data at rest is encrypted inside the volume.
All data in flight moving between the instance and the volume is encrypted.
All snapshots are encrypted.
All volumes created from the snapshot are encrypted.
To Encrypted volumes:
Create a snapshot of the unencrypted root device volume.
Copy snapshot and encrypt
Create an AMI from from encrypted snapshot
Use that AMi to launch new encrypted instances.
EC2 Hibernation:
EC2 Hibernation preserves the in-memory RAM on persistent storage(EBS)
Much faster to boot up because you do not need to reload the operating system.
Instance RAM must be less than 150GB.
Instance families include C3, C4, C5, M3, M4, M5, R3, R4 and R5.
Available for Windows, Amazon Linux 2 AMI and Ubuntu
Instances can’t be hibernated for more than 60 days.
EFS:
Support the Network File System version 4(NFSv4) protocol
Can support thousand of concurrent NFS connections
Only pay for the storage you use(no pre-provisioning required)
Data is stored across multiple AZs within a region.
Read-after-write consistency.
If you have a question around highly scalable shared storage using NFS, think EFS.
Different between EFS, FSx for Windows or FSx for Lustre.
EFS: When you need distributed, highly resilient storage for Linux instances and Linux-based applications.
Amazon FSx for Windows: When you need centralized storage for Windows-based applications, such as SharePoint, Microsoft SQL Server, Workspaces, IIS Web Server or any other native Microsoft application.
Amazon FSx for Lustre: When you need high-speed, high-capacity distributed storage. This will be applications that do high performance computing(HPC), financial modeling, etc. Remeber that FSx For Lustre can store data directly to S3.
Storage Options Use cases:
S3: used for serverless object storage.
Glacier: Used for archiving objects.
EFS: Network File System(NFS) for Linux instances. Centralized storage solution across multiple AZs.
FSx for Lustre: File storage for high performance computing Linux file systems.
EBS Volumes: Persistent storage for EC2 instances.
Instance store: Ephemeral storage for EC2 instances.
FSx for Windows: File storage for Windows instances. Centralized storage solution across multiple AZs.
Knowing the different use case for storage will gain you valuable points in the exam.
AWS Backups:
Consolidation: Use AWS Backup to Back up AWS serivces, such as EC2, EBS, EFS, Amazon FSx for Lustre, Amazon FSx for Windows File Server, and AWS Storage Gateway.
Organizations: You can use AWS Organizations in conjunction with AWS Backup to back up your different AWS services across multiple AWS accounts.
Benefits: Backup give you centralized control, letting you automate your backups and define lifecycle policies for your data. You get better compliance, as you can enforce your backup policies, ensure your backups are encrypted and audit them once complete.
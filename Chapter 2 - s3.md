# S3
- S3 is object-based stored.
- Cannot run operating or database in S3, it’s place to stored static files => file don’t change.
- Unlimited stored, up to 5TB per file stored in a bucket.
- Bucket basically is folder inside s3.
- S3 bucket have a global namespace.
- https://bucket-name.s3.region.amazoneaws.com/key-name
- S3 basically works off a key-value store:
- key(name) - value(data itself, sequence of bytes) - version ID(when enables multiple version of object) - metadata
- S3 is a safe place to store data, it spread across multiple devices and facilities to ensure availability and durability.
- Highly available and highly durable
- Standard S3:
  * High availability and Durability (>= 3 AZ): 99.99% availability and 99.9x9% durability
  * Design for frequently access data
  * Suitable for most workloads

- S3 standard suits with a lot of cases but not all case => we have 
  * Tiered Storage: s3 offers a range of storage classes designed for different use cases.
  * Lifecycle Management: Define rules to automatically transition objects to a cheaper storage tier or delete objects after a set period of time 
  * Versioning: All version of object are stored and can be retrieved including deleted objects.
- Securing data:
  * Server side cryption
  * Access control list(ACL): define which AWS accounts or groups can access data. We can attach S3 ACL to each object within a bucket.
  * Bucket policies: specify what actions are allowed or denied
- Strong read after write
  * After write or overwrite, any subsequent read request immediately get the latest version of the object.
  * Strong consistency for list operators, after a write request, you can immediately perform a listing of the objects in a bucket with all changes reflected.
- Bucket are private by default: When you create S3 bucket, it is private by default(include all object inside it). You have to allow public access on both the bucket and its object in order to make the bucket public.
- Object ACLs: You can make individual objects public using object ACLs.
- Bucket policies: You can make entire buckets public using bucket policies.
- When you upload an object to S3 and it’s successful, you will receive an HTTP 200 code
- Static content: Use S3 to host static content only(not Dynamic - got db connection)
- Automatic Scaling: S3 scales automatically with demand - don’t have to deal with load balancer, EC2 instances, provisioning
- Versioning: you can enable versioning in S3 so you can have multiple versions of an object within S3.
- Advantages:
  * All versions of object are stored in S3. This includes all writes and even if you delete an object.
  * Backup
  * Cannot be disabled - only be suspended.
  * Lifecycle rules
  * Support MFA.
- Although we have public all object in our bucket, it doesn’t apply to our previous versions of those objects.
- S3 Standard-Infrequently Access and minimize our cost
  * Rapid access: Used for data that is accessed less frequently but requires rapid access when needed.
  * You pay to Access the Data: There is a low per-GB storage price and a per-GB retrieval fee.
  * Use cases for long-term storage, backups, data store for disaster recovery files 
- S3 One zone-IA
  * Cost 20% less then S3 Standard-IA
  * Great for love-lived, infrequently access, non-critical data
- 2 Tiers:
  * Frequent and Infrequent access automatically moves your data to the most-cost effective tier based on how frequently you access each object.
  * It only cost $0.025 per 1000 objects
- Glacier Options:
  * You pay each time you access data.
  * Use only for achieve data.
  * Glacier is cheap storage.
  * Optimized for data that is very infrequently accessed.
  * 99.99% availability and 11 9’s Durability.
- And it have:
  * Option 1: Glacier Instant Retrieval provides long-term data achiving with instant retrieval time for your data
  * Option 2: Glacier Flexible Retrieval Ideal storage for archieve data does not require immediate access but needs to retrieve large sets of data at no cost, such as backup or disaster recovery use cases. Can be a minutes or up to 12 hours.
  * Option 3: Glacier Deep Archive Cheapest storage class and desgined for cútomers that retain data sets for 7-10 years or longer to meet customer needs and regulatory compliance requirements. The standard retrieval time is 12 hours, and the bulk retrieval time is 48 hours.
- Will always >= 3 AZ for each S3 Storage Classes, except S3 One Zone IA.
- Archival: Glacier
- How fast you want to be able to restore your files or it could also be what’s the cheapest option
- For S3, the most expensive is S3 Standard.
- Optiomize cost: S3 Intelligent-Tiering => going to move it around between Infrequently Accessed and S3 Standard.
- Access data sits on S3 in Standard-Infrequently Accessed as well as One Zone-Infrequently Accessed, then a retrieval fee is going to apply.
- Glacier:
  * The most expensive is S3 Glacier
  * Flexible Retrieval is slightly cheaper
  * The cheapest is Glacier Deep Archive
  * Retrieval fee is apply for 3 classes of Glacier.
- Lifecycle Management
  * Automatically moving our object between different storage tier, thereby maximizing our cost effectiveness.
  * Keep S3 Standard for 30 days, after move to S3 IA. After 90 days will move to Glacier.
  * We can use Lifecycle management with Versioning
  * Can be applied to current versions and previous versions
- Object lock to store object using Write Once, Read Many(WORM) model. It can prevent object from being deleted or modified.
- We can use S3 Object Lock to meet regulatory requirements require WORM storage, or add an extra layer of protection against object changes and deletion.
- There’s 2 different mode:
  * Governance Mode: users can’t overwrite or delete an object version or alter its lock settings unless they have special permissions.
  * Compliance mode: nobody can overwrite or delete object include root user, the retention period can’t be shortened. Compliance mode ensure that an object version can’t be overwrite or delete for the duration of the retention period.
- Legal Hold enables you to place hold on an object version. Legal hold prevents an object version from being overwritten or deleted. However, legal hold doesn’t have an associated rention period and remains in effect until removed. Legal holds can be freely placed and removed by any user who has the - s3:PutObjectLegalHold permission.
- Glacier Vault Lock is a way of applying a WORM model to Glacier.
- S3 Bucket with WORM model -> S3 Object Lock.
- Object Lock can be done on individual objects or entire bucket.
- 2 modes: Compliance mode and Governance mode
- WORM model with Glacier -> S3 Glacier Vault Lock
- There’s 3 different types of Encryption:
  * Encryption in Transit:
    * SSL/TLS
    * HTTPS
  * Encryption at Rest: Server-Side Encryption
    * SSE-S3: S3-managed keys, using AES-256 bit encryption
    * SSE-KMS: AWS key management Service-managed keys. Use key provided from AWS
    * SSE-C: use key by ourselves.
  * Encryption at Rest: Client-Side Encryption: We encrypt the file before we upload to S3.
- Enforcing Server-side Encryption: We have 2 ways to do it:
  * Console: Select the encryption setting on your s3 bucket. The easiest way is just a checkbox in the console.
  * Bucket Policy: You can also enforce encryption using a bucket policy. This method sometimes comes up in the xam.
- Everytime a file is uploaded to S3, A PUT request is initiated.
- In order to enforce server-side encryption, we’ve got 2 different options
- x-amz-server-side-encryption: If the file is to be encrypted at upload time, the x-amz-server-side-encryption parameter will be included in the request header:
  * x-amz-serverside-encryption: AES256 => use S3-managed keys
  * x-amz-server-side-encryption: aws:kms => using KMS-managed keys.
- We can create a bucket policy that denies any S3 PUT request that doesn’t include the x-amz-server-side-encryption parameter in the request header.
Note:
  * We can encryp in a number of different way:
  * Encryption in Transit: SSL/TLS, HTTPS
  * Encryption at Rest: SSE, SSE-S3, SSE-KMS, SSE-C
  * Client Side Encryption: Encrypt the files before upload to S3.
- Enforce encryption using bucket policy
- S3 prefix is just the folder inside our bucket.
- S3 has extremely low latency. You can get the first by out of S3 within 100-200ms.
- 3500 PUT/COPY/POST/DELETE and 5500 GET/HEAD requests per prefix per second.
- So we can get better performance by spreading our reads across different prefixes.
- S3 limitations when using KMS:
  * If you’re using SSE-KMS to encrypt your object, you must keep in mind the KMS limits.
  * When you upload a file, you will call GenerateDataKey in the KMS API.
  * When you download a file, you will call Decrypt in the KMS API.
- KMS comes with the build-in limits, it’s region specific:
  * Uploading/downloading will count toward the KMS quota.
  * Region-specific going to be roughly 5.500, 10k or 30k request per seconds.
  * Currently, we cannot request a quota increase for KMS.
- Encryption question tip: we might want to consider just using the native S3 encryption that’s built-in rather than using KMS. If you’re asked to troubleshoot a KMS question, it could just be that you’re hitting the KMS limit and that could be what’s causing your downloads or your requests to be much, much slower.
- S3 Multipart uploads:
  * Recommend for file over 100MB.
  * Required for file over 5GB.
  * Prallelize uploads(increase efficiency) => We have 1 big file, we split into parts and upload those chunks at the same time
- S3 Byte-Range Fetches: can be used to speed up downloads, download partial amounts of the file.
  * Parallelize downloads by specifying byte ranges. If there’s a failure in the download, it’s only for a specific byte range.
- S3 Replication used to be called Cross Region Replication because you do it from one region to another region.
- But now you can do it just from 1 bucket to another bucket in the same region as well => they renamed it.
  * It’s a way to replicate objects from one bucket to another bucket. Versioning must be enabled on both the source and destination bucket.
  * Object in an existing bucket are not replicated automatically. Once replication is turned on, all subsequent updated objects will be replicated automatically.
  * Delete markers are not replicated by default. However, we can turn on if we want => Deleting individual versions and delete markers will not be replicated by default.
- If you going to do this, it’s best to create 2 new buckets: a source bucket and a destination bucket, turn replication on and then upload your objects.
- Exam tips:
  * You can replicate object from one bucket to another.
  * Objects in an existing bucket are not replicated automatically.
  * Delete marker are not replicated by default, can enable if we want.

## networking


Networking defined

Networking is how you connect computers around the world and allow them to communicate with one another. In this course, you’ve already seen a few examples of networking. One is the AWS Global Infrastructure. AWS has built a network of resources using data centers, Availability Zones, and Regions. 

Networking basics

One way to think about networking is to think about sending a letter. When you send a letter, you provide the following three elements:


bullet
The letter, inside the envelope


bullet
The address of the sender in the from section


bullet
The address of the recipient in the to section


Each address must contain specific information:

Name of sender or recipient
Street
City
State or province
Zip, area, or postal code
Country
You need all parts of an address to ensure that your letter gets to its destination. Without the correct address, postal workers cannot properly deliver the letter. In the digital world, computers handle the delivery of messages in a similar way. This is called routing.

IP addresses

To properly route your messages to a location, you need an address. Just like each home has a mailing address, each computer has an IP address. However, instead of using the combination of street, city, state, zip code, and country, the IP address uses a combination of bits, 0s and 1s.

Here is an example of a 32-bit address in binary format:

11000000 10101000 00000001 00011110 is a 32-bit address written in binary format.
A 32-bit address written in binary format.

It’s called 32 bit because you have 32 digits. Feel free to count!

IPv4 notation

Typically, you don’t see an IP address in its binary format. Instead, it’s converted into decimal format and noted as an IPv4 address.

In the following diagram, the 32 bits are grouped into groups of 8 bits, also called octets. Each of these groups is converted into decimal format separated by a period.

An IPv4 address is written in decimal digits made up of four eight bit fields separated by a period.
An IPv4 address, for example, 192.168.1.30 is converted from four groups of eight bits.

In the end, this is what is called an IPv4 address. This is important to know when trying to communicate to a single computer. But remember, you’re working with a network. This is where Classless Inter-Domain Routing (CIDR) comes in.

CIDR notation

192.168.1.30 is a single IP address. If you want to express IP addresses between the range of 192.168.1.0 and 192.168.1.255, how can you do that?

One way is to use CIDR notation. CIDR notation is a compressed way of representing a range of IP addresses. Specifying a range determines how many IP addresses are available to you.

CIDR notation is shown here.

The number after the forward slash denotes how many bits in an IP address are fixed.
It begins with a starting IP address and is separated by a forward slash (the / character) followed by a number. The number at the end specifies how many of the bits of the IP address are fixed. In this example, the first 24 bits of the IP address are fixed. The rest (the last 8 bits) are flexible.

The last number '24' specifies that the first 24 bits of the IP address are fixed, and the last 8 bits are flexible.
32 total bits subtracted by 24 fixed bits leaves 8 flexible bits. Each of these flexible bits can be either 0 or 1, because they are binary. That means that you have two choices for each of the 8 bits, providing 256 IP addresses in that IP range.

The higher the number after the /, the smaller the number of IP addresses in your network. For example, a range of 192.168.1.0/24 is smaller than 192.168.1.0/16.

When working with networks in the AWS Cloud, you choose your network size by using CIDR notation. In AWS, the smallest IP range you can have is /28, which provides 16 IP addresses. The largest IP range you can have is a /16, which provides 65,536 IP addresses.


Amazon VPC

A virtual private cloud (VPC) is an isolated network that you create in the AWS Cloud, similar to a traditional network in a data center. When you create an Amazon VPC, you must choose three main factors:


bullet
Name of the VPC


bullet
Region where the VPC will live – A VPC spans all the Availability Zones within the selected Region.


bullet
IP range for the VPC in CIDR notation – This determines the size of your network. Each VPC can have up to five CIDRs: one primary and four secondaries for IPv4. Each of these ranges can be between /28 (in CIDR notation) and /16 in size.

Using this information, AWS will provision a network and IP addresses for that network.

When a VPC is created, you specify a CIDR block for the VPC. The VPC will span all the AZs within the selected Region.
Creating a subnet

After you create your VPC, you must create subnets inside the network. Think of subnets as smaller networks inside your base network, or virtual local area networks (VLANs) in a traditional, on-premises network. In an on-premises network, the typical use case for subnets is to isolate or optimize network traffic. In AWS, subnets are used to provide high availability and connectivity options for your resources. Use a public subnet for resources that must be connected to the internet and a private subnet for resources that won't be connected to the internet.

You can launch AWS resources, such as EC2 instances, into a specific subnet within your VPC.
When you create a subnet, you must specify the following:

VPC that you want your subnet to live in—in this case: VPC (10.0.0.0/16)
Availability Zone that you want your subnet to live in—in this case: Availability Zone 1
IPv4 CIDR block for your subnet, which must be a subset of the VPC CIDR block—in this case: 10.0.0.0/24
When you launch an EC2 instance, you launch it inside a subnet, which will be located inside the Availability Zone that you choose.

High availability with a VPC

When you create your subnets, keep high availability in mind. To maintain redundancy and fault tolerance, create at least two subnets configured in two Availability Zones.

As you learned earlier, remember that “everything fails all of the time.” With the example network, if one of the Availability Zones fails, you will still have your resources available in another Availability Zone as backup.


Reserved IPs

For AWS to configure your VPC appropriately, AWS reserves five IP addresses in each subnet. These IP addresses are used for routing, Domain Name System (DNS), and network management.

For example, consider a VPC with the IP range 10.0.0.0/22. The VPC includes 1,024 total IP addresses. This is then divided into four equal-sized subnets, each with a /24 IP range with 256 IP addresses. Out of each of those IP ranges, there are only 251 IP addresses that can be used because AWS reserves five.

AWS reserves five IP addresses in each subnet that cannot be assigned to a resource.
The five reserved IP addresses can impact how you design your network. A common starting place for those who are new to the cloud is to create a VPC with an IP range of /16 and create subnets with an IP range of /24. This provides a large amount of IP addresses to work with at both the VPC and subnet levels.

Gateways

Internet gateway
To activate internet connectivity for your VPC, you must create an internet gateway. Think of the gateway as similar to a modem. Just as a modem connects your computer to the internet, the internet gateway connects your VPC to the internet. Unlike your modem at home, which sometimes goes down or offline, an internet gateway is highly available and scalable. After you create an internet gateway, you attach it to your VPC.

An internet gateway is a VPC component that permits communication between your VPC and the internet.
A virtual private gateway is the VPN endpoint on the Amazon side of your VPN connection that can be attached to a single VPC.
Virtual private gateway
A virtual private gateway connects your VPC to another private network. When you create and attach a virtual private gateway to a VPC, the gateway acts as anchor on the AWS side of the connection. On the other side of the connection, you will need to connect a customer gateway to the other private network. A customer gateway device is a physical device or software application on your side of the connection. When you have both gateways, you can then establish an encrypted virtual private network (VPN) connection between the two sides.

AWS Direct Connect

To establish a secure physical connection between your on-premises data center and your Amazon VPC, you can use AWS Direct Connect. With AWS Direct Connect, your internal network is linked to an AWS Direct Connect location over a standard Ethernet fiber-optic cable. This connection allows you to create virtual interfaces directly to public AWS services or to your VPC.


Main route table

When you create a VPC, AWS creates a route table called the main route table. A route table contains a set of rules, called routes, that are used to determine where network traffic is directed. AWS assumes that when you create a new VPC with subnets, you want traffic to flow between them. Therefore, the default configuration of the main route table is to allow traffic between all subnets in the local network. The following rules apply to the main route table:

You cannot delete the main route table.
You cannot set a gateway route table as the main route table.
You can replace the main route table with a custom subnet route table.
You can add, remove, and modify routes in the main route table.
You can explicitly associate a subnet with the main route table, even if it's already implicitly associated.
Custom route tables

The main route table is used implicitly by subnets that do not have an explicit route table association. However, you might want to provide different routes on a per-subnet basis for traffic to access resources outside of the VPC. For example, your application might consist of a frontend and a database. You can create separate subnets for the resources and provide different routes for each of them.

If you associate a subnet with a custom route table, the subnet will use it instead of the main route table. Each custom route table that you create will have the local route already inside it, allowing communication to flow between all resources and subnets inside the VPC. You can protect your VPC by explicitly associating each new subnet with a custom route table and leaving the main route table in its original default state.




Secure subnets with network access control lists

A network ACL allows or denies specific inbound or outbound traffic at the subnet level.
Think of a network access control list (network ACL) as a virtual firewall at the subnet level. A network ACL lets you control what kind of traffic is allowed to enter or leave your subnet. You can configure this by setting up rules that define what you want to filter. Here is an example of a default ACL for a VPC that supports IPv4.

The default network ACL shown in the preceding table, allows all traffic in and out of the subnet. To allow data to flow freely to the subnet, this is a good starting place.

However, you might want to restrict data at the subnet level. For example, if you have a web application, you might restrict your network to allow HTTPS traffic and Remote Desktop Protocol (RDP) traffic to your web servers.


Network ACLs are considered stateless, so you need to include both the inbound and outbound ports used for the protocol. If you don’t include the outbound range, your server would respond but the traffic would never leave the subnet.

Because network ACLs are configured by default to allow incoming and outgoing traffic, you don’t need to change their initial settings unless you need additional security layers.

Secure EC2 instances with security groups

The next layer of security is for your EC2 instances. Here, you can create a virtual firewall called a security group. The default configuration of a security group blocks all inbound traffic and allows all outbound traffic.


By default, a security group only allows outbound traffic. To allow inbound traffic, you must create inbound rules.


You might be wondering, “Wouldn’t this block all EC2 instances from receiving the response of any customer requests?” Well, security groups are stateful. That means that they will remember if a connection is originally initiated by the EC2 instance or from the outside, and temporarily allow traffic to respond without modifying the inbound rules.

If you want your EC2 instance to accept traffic from the internet, you must open up inbound ports. If you have a web server, you might need to accept HTTP and HTTPS requests to allow that type of traffic into your security group. You can create an inbound rule that will allow port 80 (HTTP) and port 443 (HTTPS), as shown.


You learned earlier that subnets can be used to segregate traffic between computers in your network. Security groups can be used in the same way. A common design pattern is to organize resources into different groups and create security groups for each to control network communication between them.


https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html

https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html

Storage Types



AWS storage services are grouped into three categories: file storage, block storage, and object storage. In file storage, data is stored as files in a hierarchy. In block storage, data is stored in fixed-size blocks. And in object storage, data is stored as objects in buckets.


File storage

You might be familiar with file storage if you have interacted with file storage systems like Windows File Explorer or Finder on macOS. Files are organized in a tree-like hierarchy that consist of folders and subfolders. For example, if you have hundreds of cat photos on your laptop, you might want to create a folder called Cat photos, and place the images inside that folder to organize them. Because you know that these images will be used in an application, you might want to place the Cat photos folder inside another folder called Application files.

In file storage, data is stored in files, and those files are organized into a hierarchy of folders and directories.
Each file has metadata such as file name, file size, and the date the file was created. The file also has a path, for example, computer/Application_files/Cat_photos/cats-03.png. When you need to retrieve a file, your system can use the path to find it in the file hierarchy.

File storage is ideal when you require centralized access to files that must be easily shared and managed by multiple host computers. Typically, this storage is mounted onto multiple hosts, and requires file locking and integration with existing file system communication protocols.







https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html

Use cases for file storage

To learn more, expand each of the following four categories.


Web serving
–
Cloud file storage solutions follow common file-level protocols, file naming conventions, and permissions that developers are familiar with. Therefore, file storage can be integrated into web applications.



Analytics
–
Many analytics workloads interact with data through a file interface and rely on features such as file lock or writing to portions of a file. Cloud-based file storage supports common file-level protocols and has the ability to scale capacity and performance. Therefore, file storage can be conveniently integrated into analytics workflows.


Media and entertainment
–
Many businesses use a hybrid cloud deployment and need standardized access using file system protocols (NFS or SMB) or concurrent protocol access. Cloud file storage follows existing file system semantics. Therefore, storage of rich media content for processing and collaboration can be integrated for content production, digital supply chains, media streaming, broadcast playout, analytics, and archive.


Home directories
–
Businesses wanting to take advantage of the scalability and cost benefits of the cloud are extending access to home directories for many of their users. Cloud file storage systems adhere to common file-level protocols and standard permissions models. Therefore, customers can lift and shift applications that need this capability to the cloud.

Block storage

File storage treats files as a singular unit, but block storage splits files into fixed-size chunks of data called blocks that have their own addresses. Each block is an individual piece of data storage. Because each block is addressable, blocks can be retrieved efficiently. Think of block storage as a more direct route to access the data.

When data is requested, the addresses are used by the storage system to organize the blocks in the correct order to form a complete file to present back to the requestor. Besides the address, no additional metadata is associated with each block.

Changing one character in a 1-GB file with block storage


If you want to change one character in a file, you just change the block, or the piece of the file, that contains the character. This ease of access is why block storage solutions are fast and use less bandwidth.

Use cases for block storage

Because block storage is optimized for low-latency operations, it is a preferred storage choice for high-performance enterprise workloads and transactional, mission-critical, and I/O-intensive applications.



o learn more, expand each of the following three categories.


Transactional workloads
–
Organizations that process time-sensitive and mission-critical transactions store such workloads into a low-latency, high-capacity, and fault-tolerant database. Block storage allows developers to set up a robust, scalable, and highly efficient transactional database. Because each block is a self-contained unit, the database performs optimally, even when the stored data grows.


Containers
–
Developers use block storage to store containerized applications on the cloud. Containers are software packages that contain the application and its resource files for deployment in any computing environment. Like containers, block storage is equally flexible, scalable, and efficient. With block storage, developers can migrate the containers seamlessly between servers, locations, and operating environments.


Virtual machines
–
Block storage supports popular virtual machine (VM) hypervisors. Users can install the operating system, file system, and other computing resources on a block storage volume. They do so by formatting the block storage volume and turning it into a VM file system. So they can readily increase or decrease the virtual drive size and transfer the virtualized storage from one host to another.

Object storage

In object storage, files are stored as objects. Objects, much like files, are treated as a single, distinct unit of data when stored. However, unlike file storage, these objects are stored in a bucket using a flat structure, meaning there are no folders, directories, or complex hierarchies. Each object contains a unique identifier. This identifier, along with any additional metadata, is bundled with the data and stored.

Changing one character in a 1-GB file with object storage


Changing just one character in an object is more difficult than with block storage. When you want to change one character in an object, the entire object must be updated.

Use cases for object storage

With object storage, you can store almost any type of data, and there is no limit to the number of objects stored, which makes it readily scalable. Object storage is generally useful when storing large or unstructured data sets.


To learn more, expand each of the following three categories.


Data archiving
–
Cloud object storage is excellent for long-term data retention. You can cost-effectively archive large amounts of rich media content and retain mandated regulatory data for extended periods of time. You can also use cloud object storage to replace on-premises tape and disk archive infrastructure. This storage solution provides enhanced data durability, immediate retrieval times, better security and compliance, and greater data accessibility. 


Backup and recovery
–
You can configure object storage systems to replicate content so that if a physical device fails, duplicate object storage devices become available. This ensures that your systems and applications continue to run without interruption. You can also replicate data across multiple data centers and geographical regions.


Rich media
–
With object storage, you can accelerate applications and reduce the cost of storing rich media files such as videos, digital images, and music. By using storage classes and replication features, you can create cost-effective, globally replicated architecture to deliver media to distributed users.

Relating back to traditional storage systems

If you have worked with on-premises storage, you might already be familiar with block, file, and object storage. Consider the following technologies and how they relate to systems that you might have seen before:


bullet
Block storage in the cloud is analogous to direct-attached storage (DAS) or a storage area network (SAN).


bullet
File storage systems are often supported with a network-attached storage (NAS) server.

Adding storage in a traditional data center is a rigid process—the storage solutions must be purchased, installed, and configured. With cloud computing, the process is more flexible. You can create, delete, and modify storage solutions within a matter of minutes.


https://aws.amazon.com/what-is/?faq-hub-cards.sort-by=item.additionalFields.sortDate&faq-hub-cards.sort-order=desc&awsf.tech-category=tech-category%23storage


Amazon Elastic File System (Amazon EFS)

Amazon EFS icon.
Amazon Elastic File System (Amazon EFS)

Amazon Elastic File System (Amazon EFS) is a set-and-forget file system that automatically grows and shrinks as you add and remove files. There is no need for provisioning or managing storage capacity and performance. Amazon EFS can be used with AWS compute services and on-premises resources. You can connect tens, hundreds, and even thousands of compute instances to an Amazon EFS file system at the same time, and Amazon EFS can provide consistent performance to each compute instance.

With the Amazon EFS simple web interface, you can create and configure file systems quickly without any minimum fee or setup cost. You pay only for the storage used and you can choose from a range of storage classes designed to fit your use case. 



Amazon FSx

Amazon FSx icon.
Amazon FSx

Amazon FSx is a fully managed service that offers reliability, security, scalability, and a broad set of capabilities that make it convenient and cost effective to launch, run, and scale high-performance file systems in the cloud. With Amazon FSx, you can choose between four widely used file systems: Lustre, NetApp ONTAP, OpenZFS, and Windows File Server. You can choose based on your familiarity with a file system or based on your workload requirements for feature sets, performance profiles, and data management capabilities.

To learn about each file system, expand the appropriate block.

Block Storage with Amazon EC2 Instance Store and Amazon EBS


Amazon EC2 instance store

Amazon Elastic Compute Cloud (Amazon EC2) instance store provides temporary block-level storage for an instance. This storage is located on disks that are physically attached to the host computer. This ties the lifecycle of the data to the lifecycle of the EC2 instance. If you delete the instance, the instance store is also deleted. Because of this, instance store is considered ephemeral storage. Read more about it in the Amazon EC2 documentation found in the resources section at the end of this lesson.

Instance store is ideal if you host applications that replicate data to other EC2 instances, such as Hadoop clusters. For these cluster-based workloads, having the speed of locally attached volumes and the resiliency of replicated data helps you achieve data distribution at high performance. It’s also ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content.


https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1721142000/DYJ0WCj3ky3Ql5Cq38_M9g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/WlS8iIGSyUL8aDAK_poD3H2NJ-YmK1HKj.png


Amazon EBS

As the name implies, Amazon Elastic Block Store (Amazon EBS) is block-level storage that you can attach to an Amazon EC2 instance. You can compare this to how you much attach an external drive to your laptop. This attachable storage is called an EBS volume. EBS volumes act similarly to external drives in more than one way.


bullet
Detachable: You can detach an EBS volume from one EC2 instance and attach it to another EC2 instance in the same Availability Zone to access the data on it.


bullet
Distinct: The external drive is separate from the computer. That means that if an accident occurs and the computer goes down, you still have your data on your external drive. The same is true for EBS volumes.


bullet
Size-limited: You’re limited to the size of the external drive, because it has a fixed limit to how scalable it can be. For example, you might have a 2 TB external drive, which means you can only have 2 TB of content on it. This also relates to Amazon EBS, because a volume also has a max limitation of how much content you can store on it.


bullet
1-to-1 connection: Most EBS volumes can only be connected with one computer at a time. Most EBS volumes have a one-to-one relationship with EC2 instances, so they cannot be shared by or attached to multiple instances at one time.

AWS announced the Amazon EBS multi-attach feature that permits Provisioned IOPS SSD (io1 or io2) volumes to be attached to multiple EC2 instances at one time. This feature is not available for all instance types, and all instances must be in the same Availability Zone. (Read more about this in the Amazon EBS documentation in the resources section at the end of this lesson.)

Scaling Amazon EBS volumes

You can scale EBS volumes in two ways. To learn about a category, choose the appropriate tab.


Increase the volume size only if it doesn’t increase above the maximum size limit. Depending on the volume selected, Amazon EBS currently supports a maximum volume size of 64 tebibytes (TiB). For example, if you provision a 5-TiB io2 Block Express volume, you can choose to increase the size of your volume until you get to 64 TiB.


Attach multiple volumes to a single EC2 instance. Amazon EC2 has a one-to-many relationship with EBS volumes. You can add these additional volumes during or after EC2 instance creation to provide more storage capacity for your hosts.

Amazon EBS use cases

Amazon EBS is useful when you must retrieve data quickly and have data persist long term. Volumes are commonly used in the following scenarios.

To learn more, expand each of the following four categories.


Operating systems
–
Boot and root volumes can be used to store an operating system. The root device for an instance launched from an Amazon Machine Image (AMI) is typically an EBS volume. These are commonly referred to as EBS-backed AMIs.


Databases
–
As a storage layer for databases running on Amazon EC2 that will scale with your performance needs and provide consistent and low-latency performance.


Enterprise applications
–
Amazon EBS provides high availability and high durability block storage to run business-critical applications.


Big data analytics engines
–
Amazon EBS offers data persistence, dynamic performance adjustments, and the ability to detach and reattach volumes, so you can resize clusters for big data analytics.

EBS volume types

EBS volumes are organized into two main categories: solid-state drives (SSDs) and hard-disk drives (HDDs). SSDs are used for transactional workloads with frequent read/write operations with small I/O size. HDDs are used for large streaming workloads that need high throughput performance.  AWS offers two types of each.

The following two tables can help you decide which EBS volume is the right option for your workload.

Amazon EBS snapshots

Errors happen. One error is not backing up data and then inevitably losing it. To prevent this from happening to you, always back up your data, even in AWS. Because your EBS volumes consist of the data from your EC2 instance, you should make backups of these volumes, called snapshots.


EBS snapshots are incremental backups that only save the blocks on the volume that have changed after your most recent snapshot. For example, if you have 10 GB of data on a volume and only 2 GB of data have been modified since your last snapshot, only the 2 GB that have been changed are written to Amazon S3.

When you take a snapshot of any of your EBS volumes, the backups are stored redundantly in multiple Availability Zones using Amazon S3. This aspect of storing the backup in Amazon S3 is handled by AWS, so you won’t need to interact with Amazon S3 to work with your EBS snapshots. You manage them in the Amazon EBS console, which is part of the Amazon EC2 console.

EBS snapshots can be used to create multiple new volumes, whether they’re in the same Availability Zone or a different one. When you create a new volume from a snapshot, it’s an exact copy of the original volume at the time the snapshot was taken.

Object Storage with Amazon S3

Amazon S3

Unlike Amazon EBS, Amazon Simple Storage Service (Amazon S3) is a standalone storage solution that isn’t tied to compute. With Amazon S3, you can retrieve your data from anywhere on the web. If you have used an online storage service to back up the data from your local machine, you most likely have used a service similar to Amazon S3. The big difference between those online storage services and Amazon S3 is the storage type.

Amazon S3 is an object storage service. Object storage stores data in a flat structure. An object is a file combined with metadata. You can store as many of these objects as you want. All the characteristics of object storage are also characteristics of Amazon S3.

Amazon S3 concepts

Amazon S3 concepts include objects, keys, buckets, and Regions.
In Amazon S3, you store your objects in containers called buckets. You can’t upload an object, not even a single photo, to Amazon S3 without creating a bucket first. When you store an object in a bucket, the combination of a bucket name, key, and version ID uniquely identifies the object.  

When you create a bucket, you specify, at the very minimum, two details: the bucket name and the AWS Region that you want the bucket to reside in.

Amazon S3 bucket names

Amazon S3 supports global buckets. Therefore, each bucket name must be unique across all AWS accounts in all AWS Regions within a partition. A partition is a grouping of Regions, of which AWS currently has three: Standard Regions, China Regions, and AWS GovCloud (US). When naming a bucket, choose a name that is relevant to you or your business. For example, you should avoid using AWS or Amazon in your bucket name.

The following are some examples of the rules that apply for naming buckets in Amazon S3. For a full list of rules, see the link in the resources section. 

Bucket names must be between 3 (min) and 63 (max) characters long.
Bucket names can consist only of lowercase letters, numbers, dots (.), and hyphens (-).
Bucket names must begin and end with a letter or number.
Buckets must not be formatted as an IP address.
A bucket name cannot be used by another AWS account in the same partition until the bucket is deleted.
If your application automatically creates buckets, choose a bucket naming scheme that is unlikely to cause naming conflicts and will choose a different bucket name, should one not be available.

Object key names

The object key (key name) uniquely identifies the object in an Amazon S3 bucket. When you create an object, you specify the key name. As described earlier, the Amazon S3 model is a flat structure, meaning there is no hierarchy of subbuckets or subfolders. However, the Amazon S3 console does support the concept of folders. By using key name prefixes and delimiters, you can imply a logical hierarchy.  

For example, suppose your bucket called testbucket has two objects with the following object keys: 2022-03-01/AmazonS3.html and 2022-03-01/Cats.jpg. The console uses the key name prefix, 2022-03-01, and delimiter (/) to present a folder structure.

By using prefixes and delimiters, you can infer a logical hierarchy resembling folders.
Amazon S3 supports buckets and objects, and there is no hierarchy. However, by using prefixes and delimiters in an object key name, the Amazon S3 console and the AWS SDKs are able to infer hierarchy and introduce the concept of folders.

Amazon S3 use cases

Amazon S3 is a widely used storage service, with far more use cases than could fit on one screen. To learn more, expand each of the following six categories.


Backup and storage
–
Amazon S3 is a natural place to back up files because it is highly redundant. As mentioned in the last lesson, AWS stores your EBS snapshots in Amazon S3 to take advantage of its high availability.


Media hosting
–
Because you can store unlimited objects, and each individual object can be up to 5 TB, Amazon S3 is an ideal location to host video, photo, and music uploads.


Software delivery
–
You can use Amazon S3 to host your software applications that customers can download.


Data lakes
–
Amazon S3 is an optimal foundation for a data lake because of its virtually unlimited scalability. You can increase storage from gigabytes to petabytes of content, paying only for what you use.


Static websites
–
You can configure your S3 bucket to host a static website of HTML, CSS, and client-side scripts.


Static content
–
Because of the limitless scaling, the support for large files, and the fact that you can access any object over the web at any time, Amazon S3 is the perfect place to store static content.

Security in Amazon S3

Everything in Amazon S3 is private by default. This means that all Amazon S3 resources, such as buckets and objects, can only be viewed by the user or AWS account that created that resource. Amazon S3 resources are all private and protected to begin with.

If you decide that you want everyone on the internet to see your photos, you can choose to make your buckets and objects public. A public resource means that everyone on the internet can see it. Most of the time, you don’t want your permissions to be all or nothing. Typically, you want to be more granular about the way that you provide access to your resources.

By default, all Amazon S3 resources - buckets, objects, and related subresources are private. Access to resources can be granted to others by writing an access policy.
To be more specific about who can do what with your Amazon S3 resources, Amazon S3 provides several security management features: IAM policies, S3 bucket policies, and encryption to develop and implement your own security policies.

Amazon S3 and IAM policies

Previously, you learned about creating and using AWS Identity and Access Management (IAM) policies. Now you can apply that knowledge to Amazon S3. When IAM policies are attached to your resources (buckets and objects) or IAM users, groups, and roles, the policies define which actions they can perform. Access policies that you attach to your resources are referred to as resource-based policies and access policies attached to users in your account are called user policies.


You should use IAM policies for private buckets in the following two scenarios:

You have many buckets with different permission requirements. Instead of defining many different S3 bucket policies, you can use IAM policies.
You want all policies to be in a centralized location. By using IAM policies, you can manage all policy information in one location.
Amazon S3 bucket policies

Like IAM policies, S3 bucket policies are defined in a JSON format. Unlike IAM policies, which are attached to resources and users, S3 bucket policies can only be attached to S3 buckets. The policy that is placed on the bucket applies to every object in that bucket. S3 bucket policies specify what actions are allowed or denied on the bucket.


You should use S3 bucket policies in the following scenarios:

You need a simple way to do cross-account access to Amazon S3, without using IAM roles.
Your IAM policies bump up against the defined size limit. S3 bucket policies have a larger size limit.
For examples of bucket policies, see the Bucket Policy Examples(opens in a new tab) link here or in the resources section.

Amazon S3 encryption

Amazon S3 reinforces encryption in transit (as it travels to and from Amazon S3) and at rest. To protect data, Amazon S3 automatically encrypts all objects on upload and applies server-side encryption with S3-managed keys as the base level of encryption for every bucket in Amazon S3 at no additional cost.

Amazon S3 storage classes

When you upload an object to Amazon S3 and you don’t specify the storage class, you upload it to the default storage class, often referred to as standard storage. In previous lessons, you learned about the default Amazon S3 standard storage class.

Amazon S3 storage classes let you change your storage tier when your data characteristics change. For example, if you are accessing your old photos infrequently, you might want to change the storage class for the photos to save costs.

Amazon S3 versioning

As described earlier, Amazon S3 identifies objects in part by using the object name. For example, when you upload an employee photo to Amazon S3, you might name the object employee.jpg and store it in a bucket called employees. Without Amazon S3 versioning, every time you upload an object called employee.jpg to the employees bucket, it will overwrite the original object.
This can be an issue for several reasons, including the following:

Common names: The employee.jpg object name is a common name for an employee photo object. You or someone else who has access to the bucket might not have intended to overwrite it; but once it's overwritten, the original object can't be accessed.
Version preservation: You might want to preserve different versions of employee.jpg. Without versioning, if you wanted to create a new version of employee.jpg, you would need to upload the object and choose a different name for it. Having several objects all with slight differences in naming variations can cause confusion and clutter in S3 buckets.
To counteract these issues, you can use Amazon S3 versioning. Versioning keeps multiple versions of a single object in the same bucket. This preserves old versions of an object without using different names, which helps with object recovery from accidental deletions, accidental overwrites, or application failures.

Keep multiple versions of a single object in the same bucket.
If you enable versioning for a bucket, Amazon S3 automatically generates a unique version ID for the object. In one bucket, for example, you can have two objects with the same key but different version IDs, such as employeephoto.jpg (version 111111) and employeephoto.jpg (version 121212).

By using versioning-enabled buckets, you can recover objects from accidental deletion or overwrite. The following are examples:


bullet
Deleting an object does not remove the object permanently. Instead, Amazon S3 puts a marker on the object that shows that you tried to delete it. If you want to restore the object, you can remove the marker and the object is reinstated.


bullet
If you overwrite an object, it results in a new object version in the bucket. You still have access to previous versions of the object.

Versioning states

Buckets can be in one of three states. The versioning state applies to all objects in the bucket. Storage costs are incurred for all objects in your bucket, including all versions. To reduce your Amazon S3 bill, you might want to delete previous versions of your objects when they are no longer needed.


Managing your storage lifecycle

If you keep manually changing your objects, such as your employee photos, from storage tier to storage tier, you might want to automate the process by configuring their Amazon S3 lifecycle. When you define a lifecycle configuration for an object or group of objects, you can choose to automate between two types of actions: transition and expiration.

Transition actions define when objects should transition to another storage class.
Expiration actions define when objects expire and should be permanently deleted.
For example, you might transition objects to S3 Standard-IA storage class 30 days after you create them. Or you might archive objects to the S3 Glacier Deep Archive storage class 1 year after creating them.

Select transition and expiration actions for objects with storage lifecycles.
The following use cases are good candidates for the use of lifecycle configuration rules:

Periodic logs: If you upload periodic logs to a bucket, your application might need them for a week or a month. After that, you might want to delete them.
Data that changes in access frequency: Some documents are frequently accessed for a limited period of time. After that, they are infrequently accessed. At some point, you might not need real-time access to them. But your organization or regulations might require you to archive them for a specific period. After that, you can delete them.


https://aws.amazon.com/s3/storage-classes/

https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/example-bucket-policies.html


Amazon EC2 instance store
Instance store is ephemeral block storage. This is preconfigured storage that exists on the same physical server that hosts the EC2 instance and cannot be detached from Amazon EC2. You can think of it as a built-in drive for your EC2 instance.

 

Instance store is generally well suited for temporary storage of information that is constantly changing, such as buffers, caches, and scratch data. It is not meant for data that is persistent or long lasting. If you need persistent long-term block storage that can be detached from Amazon EC2 and provide you more management flexibility, such as increasing volume size or creating snapshots, you should use Amazon EBS.


Amazon EBS
Amazon EBS is meant for data that changes frequently and must persist through instance stops, terminations, or hardware failures. Amazon EBS has two types of volumes: SSD-backed volumes and HDD-backed volumes.



The performance of SSD-backed volumes depends on the IOPs and is ideal for transactional workloads, such as databases and boot volumes. 



The performance of HDD-backed volumes depends on megabytes per second (MBps) and is ideal for throughput-intensive workloads, such as big data, data warehouses, log processing, and sequential data I/O.



Here are a few important features of Amazon EBS that you need to know when comparing it to other services.

It is block storage.
You pay for what you provision (you have to provision storage in advance).
EBS volumes are replicated across multiple servers in a single Availability Zone.
Most EBS volumes can only be attached to a single EC2 instance at a time.

Amazon S3
If your data doesn’t change often, Amazon S3 might be a cost-effective and scalable storage solution for you. Amazon S3 is ideal for storing static web content and media, backups and archiving, and data for analytics. It can also host entire static websites with custom domain names.



Here are a few important features of Amazon S3 to know about when comparing it to other services:

It is object storage.
You pay for what you use (you don’t have to provision storage in advance).
Amazon S3 replicates your objects across multiple Availability Zones in a Region.
Amazon S3 is not storage attached to compute.

Amazon EFS
Amazon EFS provides highly optimized file storage for a broad range of workloads and applications. It is the only cloud-native shared file system with fully automatic lifecycle management. Amazon EFS file systems can automatically scale from gigabytes to petabytes of data without needing to provision storage. Tens, hundreds, or even thousands of compute instances can access an Amazon EFS file system at the same time.



Amazon EFS Standard storage classes are ideal for workloads that require the highest levels of durability and availability. EFS One Zone storage classes are ideal for workloads such as development, build, and staging environments.



Here are a few important features of Amazon EFS to know about when comparing it to other services:

It is file storage.
Amazon EFS is elastic, and automatically scales up or down as you add or remove files. And you pay only for what you use.
Amazon EFS is highly available and designed to be highly durable. All files and directories are redundantly stored within and across multiple Availability Zones. 
Amazon EFS offers native lifecyle management of your files and a range of storage classes to choose from.

Amazon FSx
Amazon FSx provides native compatibility with third-party file systems. You can choose from NetApp ONTAP, OpenZFS, Windows File Server, and Lustre. With Amazon FSx, you don't need to worry about managing file servers and storage. This is because Amazon FSx automates time consuming administration task such as hardware provisioning, software configuration, patching, and backups. This frees you up to focus on your applications, end users, and business.



Amazon FSx file systems offer feature sets, performance profiles, and data management capabilities that support a wide variety of use cases and workloads. Examples include machine learning, analytics, high performance computing (HPC) applications, and media and entertainment.  

Databases on AWS



History behind enterprise databases

Choosing a database used to be a straightforward decision. Customers had only a few options to choose from. Typically, they would consider a few vendors and then, inevitably, choose one for all their applications. Businesses often selected a database technology before they fully understood their use case. Since the 1970s, the database type most commonly selected by businesses was a relational database.

Relational databases

A relational database organizes data into tables. Data in one table can link to data in other tables to create relationships—hence, the relational part of the name.

A table stores data in rows and columns. A row, often called a record, contains all information about a specific entry. Columns describe attributes of an entry. The following image is an example of three tables in a relational database.

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1721142000/DYJ0WCj3ky3Ql5Cq38_M9g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/OLsaStAvUCWO8Qnp_2LDugnFFKSyS9mOy.png


The preceding image shows a table for books, a table for sales, and a table for authors. In the books table, each row includes the International Standard Book Number (ISBN), title, author, and format. Each of these attributes is stored in its own column. The books table has something in common with the other two tables—the author attribute. That common column creates a relationship between the tables.

The tables, rows, columns, and relationships between them is called a logical schema. With relational databases, a schema is fixed. After the database is operational, it becomes difficult to change the schema. Because of this, most of the data modeling is done up front before the database is active.

Relational database management system

With a relational database management system (RDBMS), you can create, update, and administer a relational database. Some common examples of RDBMSs include the following:

MySQL
PostgresQL
Oracle
Microsoft SQL Server
Amazon Aurora
You communicate with an RDBMS by using structured query language (SQL) queries, similar to the following example:

SELECT * FROM table_name.

This query selects all the data from a particular table. However, the power of SQL queries is in creating more complex queries that pull data from several tables to identify patterns and answers to business problems. For example, querying the sales table and the books table together to see sales in relation to an author’s books. Querying tables together to better understand their relationships is made possible by a "join".

Relational database benefits

To learn more about the benefits of using relational databases, flip each of the following flashcards by choosing them. 



Relational database benefits

To learn more about the benefits of using relational databases, flip each of the following flashcards by choosing them. 

Front of card
Complex SQL


Click to flip
Back of card
With SQL, you can join multiple tables so you can better understand relationships between your data.


Click to flip
Front of card
Reduced redundancy


Click to flip
Back of card
You can store data in one table and reference it from other tables instead of saving the same data in different places.


Click to flip
Front of card
Familiarity


Click to flip
Back of card
Because relational databases have been a popular choice since the 1970s, technical professionals often have familiarity and experience with them.


Click to flip
Front of card
Accuracy


Click to flip
Back of card
Relational databases ensure that your data has high integrity and adheres to the atomicity, consistency, isolation, and durability (ACID) principle.


Click to flip
Relational database use cases

Much of the world runs on relational databases. In fact, they’re at the core of many mission-critical applications, some of which you might use in your day-to-day life.

To learn some common use cases for relational databases, expand each of the following two categories.

To learn some common use cases for relational databases, expand each of the following two categories.


Applications that have a fixed schema
–
These are applications that have a fixed schema and don't change often. An example is a lift-and-shift application that lifts an app from on-premises and shifts it to the cloud, with little or no modifications.


Applications that need persistent storage
–
These are applications that need persistent storage and follow the ACID principle, such as:

Enterprise resource planning (ERP) applications
Customer relationship management (CRM) applications
Commerce and financial applications
Choose between unmanaged and managed databases

If you want to trade your on-premises database for a relational database on AWS, you first need to select how you want to run it—managed or unmanaged. Managed services and unmanaged services are handled similar to the shared responsibility model. The shared responsibility model distinguishes between AWS security responsibilities and the customer’s security responsibilities. Likewise, managed compared to unmanaged can be understood as a trade-off between convenience and control.

Unmanaged databases

If you operate a relational database on premises, you are responsible for all aspects of operation. This includes data center security and electricity, host machines management, database management, query optimization, and customer data management. You are responsible for absolutely everything, which means you have control over absolutely everything.

Now, suppose you want to shift some of the work to AWS by running your relational database on Amazon Elastic Compute Cloud (Amazon EC2). If you host a database on Amazon EC2, AWS implements and maintains the physical infrastructure and hardware and installs the EC2 instance operating system (OS). However, you are still responsible for managing the EC2 instance, managing the database on that host, optimizing queries, and managing customer data.

This is called an unmanaged database option. In this option, AWS is responsible for and has control over the hardware and underlying infrastructure. You are responsible for and have control over management of the host and database.


https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1721142000/DYJ0WCj3ky3Ql5Cq38_M9g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/tCWAW7N_ulNvnDIJ_qnA3DCLuIj69t7zG.png

You are responsible for everything in a database hosted on-premises. AWS takes on more of that responsibility in databases hosted in Amazon EC2.

Managed databases

To shift more of the work to AWS, you can use a managed database service. These services provide the setup of both the EC2 instance and the database, and they provide systems for high availability, scalability, patching, and backups. However, in this model, you’re still responsible for database tuning, query optimization, and ensuring that your customer data is secure. This option provides the ultimate convenience but the least amount of control compared to the two previous options.

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1721142000/DYJ0WCj3ky3Ql5Cq38_M9g/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/OSKho6F8uXYdN76j_AOuKIausIFuSmauW.png


Amazon RDS overview

Amazon RDS icon
Amazon Relational Database Service (Amazon RDS)

Amazon RDS is a managed database service customers can use to create and manage relational databases in the cloud without the operational burden of traditional database management. For example, imagine you sell healthcare equipment, and your goal is to be the number-one seller on the West Coast of the United States. Building a database doesn’t directly help you achieve that goal. However, having a database is a necessary component to achieving that goal. 

With Amazon RDS, you can offload some of the unrelated work of creating and managing a database. You can focus on the tasks that differentiate your application, instead of focusing on infrastructure-related tasks, like provisioning, patching, scaling, and restoring.

Amazon RDS supports most of the popular RDBMSs, ranging from commercial options to open-source options and even a specific AWS option. Supported Amazon RDS engines include the following:

Commercial: Oracle, SQL Server
Open source: MySQL, PostgreSQL, MariaDB
Cloud native: Aurora 


Database instances

Just like the databases you build and manage yourself, Amazon RDS is built from compute and storage. The compute portion is called the database (DB) instance, which runs the DB engine. Depending on the engine selected, the instance will have different supported features and configurations. A DB instance can contain multiple databases with the same engine, and each DB can contain multiple tables.

Underneath the DB instance is an EC2 instance. However, this instance is managed through the Amazon RDS console instead of the Amazon EC2 console. When you create your DB instance, you choose the instance type and size. The DB instance class you choose affects how much processing power and memory it has.


Storage on Amazon RDS

The storage portion of DB instances for Amazon RDS use Amazon Elastic Block Store (Amazon EBS) volumes for database and log storage. This includes MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server. 

When using Aurora, data is stored in cluster volumes, which are single, virtual volumes that use solid-state drives (SSDs). A cluster volume contains copies of your data across three Availability Zones in a single AWS Region. For nonpersistent, temporary files, Aurora uses local storage.

Amazon RDS provides three storage types: General Purpose SSD (also called gp2 and gp3), Provisioned IOPS SSD (also called io1), and Magnetic (also called standard). They differ in performance characteristics and price, which means you can tailor your storage performance and cost to the needs of your database workload.


Amazon RDS in an Amazon Virtual Private Cloud

When you create a DB instance, you select the Amazon Virtual Private Cloud (Amazon VPC) your databases will live in. Then, you select the subnets that will be designated for your DB. This is called a DB subnet group, and it has at least two Availability Zones in its Region. The subnets in a DB subnet group should be private, so they don’t have a route to the internet gateway. This ensures that your DB instance, and the data inside it, can be reached only by the application backend.

Access to the DB instance can be restricted further by using network access control lists (network ACLs) and security groups. With these firewalls, you can control, at a granular level, the type of traffic you want to provide access into your database.

Using these controls provides layers of security for your infrastructure. It reinforces that only the backend instances have access to the database.

Backup data

You don’t want to lose your data. To take regular backups of your Amazon RDS instance, you can use automated backups or manual snapshots. To learn about a category, choose the appropriate tab.

Automated backups are turned on by default. This backs up your entire DB instance (not just individual databases on the instance) and your transaction logs. When you create your DB instance, you set a backup window that is the period of time that automatic backups occur. Typically, you want to set the window during a time when your database experiences little activity because it can cause increased latency and downtime.

Retaining backups: Automated backups are retained between 0 and 35 days. You might ask yourself, “Why set automated backups for 0 days?” The 0 days setting stops automated backups from happening. If you set it to 0, it will also delete all existing automated backups. This is not ideal. The benefit of automated backups that you can do point-in-time recovery.



Point-in-time recovery: This creates a new DB instance using data restored from a specific point in time. This restoration method provides more granularity by restoring the full backup and rolling back transactions up to the specified time range.

If you want to keep your automated backups longer than 35 days, use manual snapshots. Manual snapshots are similar to taking Amazon EBS snapshots, except you manage them in the Amazon RDS console. These are backups that you can initiate at any time. They exist until you delete them. For example, to meet a compliance requirement that mandates you to keep database backups for a year, you need to use manual snapshots. If you restore data from a manual snapshot, it creates a new DB instance using the data from the snapshot.


Choosing a backup option

It is advisable to deploy both backup options. Automated backups are beneficial for point-in-time recovery. With manual snapshots, you can retain backups for longer than 35 days. 

Redundancy with Amazon RDS Multi-AZ

In an Amazon RDS Multi-AZ deployment, Amazon RDS creates a redundant copy of your database in another Availability Zone. You end up with two copies of your database—a primary copy in a subnet in one Availability Zone and a standby copy in a subnet in a second Availability Zone.

The primary copy of your database provides access to your data so that applications can query and display the information. The data in the primary copy is synchronously replicated to the standby copy. The standby copy is not considered an active database, and it does not get queried by applications.

Diagram depicting Amazon RDS Multi-AZ creating a redundant copy of a database in another Availability Zone.
To improve availability, Amazon RDS Multi-AZ ensures that you have two copies of your database running and that one of them is in the primary role. If an availability issue arises, such as the primary database loses connectivity, Amazon RDS initiates an automatic failover.

When you create a DB instance, a Domain Name System (DNS) name is provided. AWS uses that DNS name to fail over to the standby database. In an automatic failover, the standby database is promoted to the primary role, and queries are redirected to the new primary database.

To help ensure that you don't lose Multi-AZ configuration, there are two ways you can create a new standby database. They are as follows:

Demote the previous primary to standby if it's still up and running.
Stand up a new standby DB instance.
The reason you can select multiple subnets for an Amazon RDS database is because of the Multi-AZ configuration. You will want to ensure that you have subnets in different Availability Zones for your primary and standby copies.

Amazon RDS security

When it comes to security in Amazon RDS, you have control over managing access to your Amazon RDS resources, such as your databases on a DB instance. How you manage access will depend on the tasks you or other users need to perform in Amazon RDS. Network ACLs and security groups help users dictate the flow of traffic. If you want to restrict the actions and resources others can access, you can use AWS Identity and Access Management (IAM) policies. 


Purpose-built databases for all application needs

We covered Amazon RDS and relational databases in the previous lesson, and for a long time, relational databases were the default option. They were widely used in nearly all applications. A relational database is like a multi-tool. It can do many things, but it is not perfectly suited to any one particular task. It might not always be the best choice for your business needs. 

The one-size-fits-all approach of using a relational database for everything no longer works. Over the past few decades, there has been a shift in the database landscape, and this shift has led to the rise of purpose-built databases. Developers can consider the needs of their application and choose a database that will fit those needs. 

AWS offers a broad and deep portfolio of purpose-built databases that support diverse data models. Customers can use them to build data-driven, highly scalable, distributed applications. You can pick the best database to solve a specific problem and break away from restrictive commercial databases. You can focus on building applications that meet the needs of your organization.

DynamoDB overview

DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. With DynamoDB, you can offload the administrative burdens of operating and scaling a distributed database. You don't need to worry about hardware provisioning, setup and configuration, replication, software patching, or cluster scaling.

Amazon DynamoDB icon.
Amazon DynamoDB

With DynamoDB, you can do the following:

Create database tables that can store and retrieve any amount of data and serve any level of request traffic. 
Scale up or scale down your tables' throughput capacity without downtime or performance degradation. 
Monitor resource usage and performance metrics using the AWS Management Console.
DynamoDB automatically spreads the data and traffic for your tables over a sufficient number of servers to handle your throughput and storage requirements. It does this while maintaining consistent, fast performance. All your data is stored on SSDs and is automatically replicated across multiple Availability Zones in a Region, providing built-in high availability and data durability.

DynamoDB core components

In DynamoDB, tables, items, and attributes are the core components that you work with. A table is a collection of items, and each item is a collection of attributes. DynamoDB uses primary keys to uniquely identify each item in a table and secondary indexes to provide more querying flexibility.

To learn more, choose each of the three numbered markers.  




DynamoDB use cases

DynamoDB is a fully managed service that handles the operations work. You can offload the administrative burdens of operating and scaling distributed databases to AWS.

You might want to consider using DynamoDB in the following circumstances:


bullet
You are experiencing scalability problems with other traditional database systems.


bullet
You are actively engaged in developing an application or service.


bullet
You are working with an OLTP workload.


bullet
You care deploying a mission-critical application that must be highly available at all times without manual intervention.


bullet
You require a high level of data durability, regardless of your backup-and-restore strategy.

DynamoDB is used in a wide range of workloads because of its simplicity, from low-scale operations to ultrahigh-scale operations, such as those demanded by Amazon.com. 

To learn more about potential use cases, expand each of the following four categories.

To learn more about potential use cases, expand each of the following four categories.


Develop software applications
–
Build internet-scale applications supporting user-content metadata and caches that require high concurrency and connections for millions of users and millions of requests per second.


Create media metadata stores
–
Scale throughput and concurrency for analysis of media and entertainment workloads, such as real-time video streaming and interactive content. Deliver lower latency with multi-Region replication across Regions.


Scale gaming platforms
–
Focus on driving innovation with no operational overhead. Build out your game platform with player data, session history, and leaderboards for millions of concurrent users.


Deliver seamless retail experiences
–
Use design patterns for deploying shopping carts, workflow engines, inventory tracking, and customer profiles. DynamoDB supports high-traffic, extreme-scaled events and can handle millions of queries per second.


DynamoDB security

DynamoDB provides a number of security features to consider as you develop and implement your own security policies. They include the following:


bullet
DynamoDB provides a highly durable storage infrastructure designed for mission-critical and primary data storage. Data is redundantly stored on multiple devices across multiple facilities in a DynamoDB Region.  


bullet
All user data stored in DynamoDB is fully encrypted at rest. DynamoDB encryption at rest provides enhanced security by encrypting all your data at rest using encryption keys stored in AWS Key Management Service (AWS KMS).


bullet
IAM administrators control who can be authenticated and authorized to use DynamoDB resources. You can use IAM to manage access permissions and implement security policies.


bullet
As a managed service, DynamoDB is protected by the AWS global network security procedures.








https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html



Choose the database service that is the best fit for the job to help you optimize scale, performance, and costs when designing applications.


AWS database services

As we learned in the previous lessons, AWS has a variety of database options for different use cases. The following table provides a quick look at the AWS database portfolio.

Breaking up applications and databases

As the industry changes, applications and databases change too. Today, with larger applications, you no longer see just one database supporting them. Instead, applications are broken into smaller services, each with its own purpose-built database supporting it. This shift removes the idea of a one-size-fits-all database and replaces it with a complimentary database strategy. You can give each database the appropriate functionality, performance, and scale the workload requires.


Monitoring
Purpose of monitoring

When operating a website like the employee directory application on AWS, you might have questions like the following:

How many people are visiting my site day to day?
How can I track the number of visitors over time?
How will I know if the website is having performance or availability issues?
What happens if my Amazon Elastic Compute Cloud (Amazon EC2) instance runs out of capacity?
Will I be alerted if my website goes down?
You need a way to collect and analyze data about the operational health and usage of your resources. The act of collecting, analyzing, and using data to make decisions or answer questions about your IT resources and systems is called monitoring.

Monitoring provides a near real-time pulse on your system and helps answer the previous questions. You can use the data you collect to watch for operational issues caused by events like overuse of resources, application flaws, resource misconfiguration, or security-related events. Think of the data collected through monitoring as outputs of the system, or metrics.

Use metrics to solve problems

The AWS resources that host your solutions create various forms of data that you might be interested in collecting. Each individual data point that a resource creates is a metric. Metrics that are collected and analyzed over time become statistics, such as average CPU utilization over time showing a spike.

Graph depicting a spike in CPU utilization.
One way to evaluate the health of an EC2 instance is through CPU utilization. Generally speaking, if an EC2 instance has a high CPU utilization, it can mean a flood of requests. Or it can reflect a process that has encountered an error and is consuming too much of the CPU. When analyzing CPU utilization, take a process that exceeds a specific threshold for an unusual length of time. Use that abnormal event as a cue to either manually or automatically resolve the issue through actions like scaling the instance.

CPU utilization is one example of a metric. Other examples of metrics that EC2 instances have are network utilization, disk performance, memory utilization, and the logs created by the applications running on top of Amazon EC2.

Types of metrics

Different resources in AWS create different types of metrics. To see examples of metrics associated with different resources, flip each of the following flashcards by choosing them. 

Amazon Simple Storage Service (Amazon S3) metrics
Size of objects stored in a bucket
Number of objects stored in a bucket
Number of HTTP request made to a bucket

Amazon Relational Database Service (Amazon RDS) metrics



Database connections
CPU utilization of an instance
Disk space consumption


Amazon EC2 metrics
CPU utilization
Network utilization
Disk performance
Status checks

This is not a complete list of metrics for any of the services mentioned, but you can see how different resources create different metrics. You might be interested in a wide variety of metrics depending on your resources, goals, and questions.

Monitoring benefits

Monitoring gives you visibility into your resources, but the question now is, "Why is that important?" This section describes some of the benefits of monitoring.

To learn more, expand each of the following five categories.


Respond proactively
–
Respond to operational issues proactively before your end users are aware of them. Waiting for end users to let you know when your application is experiencing an outage is a bad practice. Through monitoring, you can keep tabs on metrics like error response rate and request latency. Over time, the metrics help signal when an outage is going to occur. You can automatically or manually perform actions to prevent the outage from happening and fix the problem before your end users are aware of it.


Improve performance and reliability
–
Monitoring can improve the performance and reliability of your resources. Monitoring the various resources that comprise your application provides you with a full picture of how your solution behaves as a system. Monitoring, if done well, can illuminate bottlenecks and inefficient architectures. This helps you drive performance and improve reliability.


Recognize security threats and events
–
By monitoring, you can recognize security threats and events. When you monitor resources, events, and systems over time, you create what is called a baseline. A baseline defines normal activity. Using a baseline, you can spot anomalies like unusual traffic spikes or unusual IP addresses accessing your resources. When an anomaly occurs, an alert can be sent out or an action can be taken to investigate the event.


Make data-driven decisions
–
Monitoring helps you make data-driven decisions for your business. Monitoring keeps an eye on IT operational health and drives business decisions. For example, suppose you launched a new feature for your cat photo app and now you want to know if it’s being used. You can collect application-level metrics and view the number of users who use the new feature. With your findings, you can decide whether to invest more time into improving the new feature.


Create cost-effective solutions
–
Through monitoring, you can create more cost-effective solutions. You can view resources that are underused and rightsize your resources to your usage. This helps you optimize cost and make sure you aren’t spending more money than necessary.


Amazon CloudWatch

Visibility using CloudWatch

AWS resources create data that you can monitor through metrics, logs, network traffic, events, and more. This data comes from components that are distributed in nature. This can lead to difficulty in collecting the data you need if you don’t have a centralized place to review it all. AWS has taken care of centralizing the data collection for you with a service called CloudWatch.

Amazon CloudWatch icon.
Amazon CloudWatch

CloudWatch is a monitoring and observability service that collects your resource data and provides actionable insights into your applications. With CloudWatch, you can respond to system-wide performance changes, optimize resource usage, and get a unified view of operational health.

You can use CloudWatch to do the following:


bullet
Detect anomalous behavior in your environments.


bullet
Set alarms to alert you when something is not right.


bullet
Visualize logs and metrics with the AWS Management Console.


bullet
Take automated actions like scaling.


bullet
Troubleshoot issues.


bullet
Discover insights to keep your applications healthy.

How CloudWatch works

With CloudWatch, all you need to get started is an AWS account. It is a managed service that you can use for monitoring without managing the underlying infrastructure.








The employee directory application is built with various AWS services working together as building blocks. Monitoring the individual services independently can be challenging. Fortunately, CloudWatch acts as a centralized place where metrics are gathered and analyzed. 


Many AWS services automatically send metrics to CloudWatch for free at a rate of 1 data point per metric per 5-minute interval. This is called basic monitoring, and it gives you visibility into your systems without any extra cost. For many applications, basic monitoring is adequate.

For applications running on EC2 instances, you can get more granularity by posting metrics every minute instead of every 5-minutes using a feature like detailed monitoring. Detailed monitoring incurs a fee. For more information about pricing, see "Amazon CloudWatch Pricing" in the Resources section at the end of this lesson.


CloudWatch concepts

Metrics are the fundamental concept in CloudWatch. A metric represents a time-ordered set of data points that are published to CloudWatch. Think of a metric as a variable to monitor and the data points as representing the values of that variable over time. Every metric data point must be associated with a timestamp.

To learn more, choose each numbered marker.





AWS services that send data to CloudWatch attach dimensions to each metric. A dimension is a name and value pair that is part of the metric’s identity. You can use dimensions to filter the results that CloudWatch returns. For example, many Amazon EC2 metrics publish InstanceId as a dimension name and the actual instance ID as the value for that dimension.

Screenshot depicting the metrics and dimensions used to filter the results that CloudWatch returns.
By default, many AWS services provide metrics at no charge for resources such as EC2 instances, Amazon Elastic Block Store (Amazon EBS) volumes, and Amazon RDS database (DB) instances. For a charge, you can activate features such as detailed monitoring or publishing your own application metrics on resources such as your EC2 instances. 

Custom metrics

Suppose you have an application, and you want to record the number of page views your website gets. How would you record this metric with CloudWatch? First, it's an application-level metric. That means it’s not something the EC2 instance would post to CloudWatch by default. This is where custom metrics come in. With custom metrics, you can publish your own metrics to CloudWatch.

If you want to gain more granular visibility, you can use high-resolution custom metrics, which make it possible for you to collect custom metrics down to a 1-second resolution. This means you can send 1 data point per second per custom metric.

Some examples of custom metrics include the following:


bullet
Webpage load times


bullet
Request error rates


bullet
Number of processes or threads on your instance


bullet
Amount of work performed by your application

CloudWatch dashboards

Once you provision your AWS resources and they are sending metrics to CloudWatch, you can visualize and review that data using CloudWatch dashboards. Dashboards are customizable home pages you can configure for data visualization for one or more metrics through widgets, such as a graph or text.

You can build many custom dashboards, each one focusing on a distinct view of your environment. You can even pull data from different AWS Regions into a single dashboard to create a global view of your architecture. The following screenshot an example of a dashboard with metrics from Amazon EC2 and Amazon EBS.

Screenshot of a CloudWatch dashboard used to create customized views of the metrics and alarms for AWS resources.
CloudWatch aggregates statistics according to the period of time that you specify when creating your graph or requesting your metrics. You can also choose whether your metric widgets display live data. Live data is data published within the last minute that has not been fully aggregated.

You are not bound to using CloudWatch exclusively for all your visualization needs. You can use external or custom tools to ingest and analyze CloudWatch metrics using the GetMetricData API.

As far as security is concerned, with AWS Identity and Access Management (IAM) policies, you control who has access to view or manage your CloudWatch dashboards.

Amazon CloudWatch Logs

CloudWatch Logs is centralized place for logs to be stored and analyzed. With this service, you can monitor, store, and access your log files from applications running on EC2 instances, AWS Lambda functions, and other sources.

Screenshot of CloudWatch Logs with centralized logs from all systems, applications, and AWS services in a single service.
With CloudWatch Logs, you can query and filter your log data. For example, suppose you’re looking into an application logic error for your application. You know that when this error occurs, it will log the stack trace. Because you know it logs the error, you query your logs in CloudWatch Logs to find the stack trace. You also set up metric filters on logs, which turn log data into numerical CloudWatch metrics that you can graph and use on your dashboards.

Some services, like Lambda, are set up to send log data to CloudWatch Logs with minimal effort. With Lambda, all you need to do is give the Lambda function the correct IAM permissions to post logs to CloudWatch Logs. Other services require more configuration. For example, to send your application logs from an EC2 instance into CloudWatch Logs, you need to install and configure the CloudWatch Logs agent on the EC2 instance. With the CloudWatch Logs agent, EC2 instances can automatically send log data to CloudWatch Logs.

CloudWatch Logs terminology

Log data sent to CloudWatch Logs can come from different sources, so it’s important you understand how they’re organized. 

To learn more about logs terminology, choose each of the three numbered markers.








CloudWatch alarms

You can create CloudWatch alarms to automatically initiate actions based on sustained state changes of your metrics. You configure when alarms are invoked and the action that is performed.

First, you must decide which metric you want to set up an alarm for, and then you define the threshold that will invoke the alarm. Next, you define the threshold's time period. For example, suppose you want to set up an alarm for an EC2 instance to invoke when the CPU utilization goes over a threshold of 80 percent. You also must specify the time period the CPU utilization is over the threshold. 

You don’t want to invoke an alarm based on short, temporary spikes in the CPU. You only want to invoke an alarm if the CPU is elevated for a sustained amount of time. For example, if CPU utilization exceeds 80 percent for 5 minutes or longer, there might be a resource issue. To set up an alarm you need to choose the metric, threshold, and time period.

Screenshot depicting how to specify the metric and the conditions in CloudWatch.
An alarm can be invoked when it transitions from one state to another. After an alarm is invoked, it can initiate an action. Actions can be an Amazon EC2 action, an automatic scaling action, or a notification sent to Amazon Simple Notification Service (Amazon SNS).

To learn more about the three possible states of an alarm, flip each of the following flashcards by choosing them. 

Front of card
OK


Click to flip
Back of card
The metric is within the defined threshold. Everything appears to be operating like normal.


Click to flip
Front of card
ALARM


Click to flip
Back of card
The metric is outside the defined threshold. This might be an operational issue.


Click to flip
Front of card
INSUFFICIENT_DATA


Click to flip
Back of card
The alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state.


Click to flip
Prevent and troubleshoot issues with CloudWatch alarms

CloudWatch Logs uses metric filters to turn the log data into metrics that you can graph or set an alarm on. The following timeline indicates the order of the steps to complete when setting up an alarm. It also provides an example using our employee directory application.

1
Set up a metric filter
For the employee directory application, suppose you set up a metric filter for HTTP 500 error response codes. 

2
Define an alarm
Then, you define which metric alarm state should be invoked based on the threshold. With this example, the alarm state is invoked if HTTP 500 error responses are sustained for a specified period of time.

3
Define an action
Next, you define an action that you want to take place when the alarm is invoked. Here, it makes sense to send an email or text alert to you so you can start troubleshooting the website. Hopefully, you can fix it before it becomes a bigger issue.



After the alarm is set up, you know that if the error happens again, you will be notified promptly.

You can set up different alarms for different reasons to help you prevent or troubleshoot operational issues. In the scenario just described, the alarm invokes an Amazon SNS notification that goes to a person who looks into the issue manually. 

Another option is to have alarms invoke actions that automatically remediate technical issues. For example, you can set up an alarm to invoke an EC2 instance to reboot or scale services up or down. You can even set up an alarm to invoke an Amazon SNS notification that invokes a Lambda function. The Lambda function then calls any AWS API to manage your resources and troubleshoot operational issues. By using AWS services together like this, you can respond to events more quickly.














https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring_best_practices.html

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring_ec2.html
https://docs.aws.amazon.com/AmazonS3/latest/userguide/monitoring-overview.html
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Monitoring.html



https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_RDS_Configuring.html

https://docs.aws.amazon.com//AmazonRDS/latest/UserGuide/UsingWithRDS.html

https://aws.amazon.com/products/databases/


https://aws.amazon.com/relational-database/




https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/GettingStarted.html















https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Storage.html






















https://aws.amazon.com/efs/



https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html

https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html





Resources
https://web.stanford.edu/class/cs101/network-1-introduction.html

https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html

https://cidr.xyz/
https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
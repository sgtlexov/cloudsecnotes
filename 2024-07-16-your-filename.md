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







https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Storage.html






















https://aws.amazon.com/efs/



https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html

https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html





Resources
https://web.stanford.edu/class/cs101/network-1-introduction.html

https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html

https://cidr.xyz/
https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
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
























Resources
https://web.stanford.edu/class/cs101/network-1-introduction.html

https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html

https://cidr.xyz/
https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
## Compute as a Service
Servers

The first building block that you need to host an application is a server. Servers can usually handle HTTP requests and send responses to clients following the client-server model. Although any API-based communication also falls under this model. 

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720936800/AXq6iF0MGvKt5w_wALPgYw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/bkmed5oahZm3RlXb_pTtbd7zybSuD-m3K.png


A client is a person or computer that sends a request. A server handling the requests is a computer, or collection of computers, connected to the internet serving websites to internet users. Servers power your application by providing CPU, memory, and networking capacity to process users’ requests and transform them into responses. For context, common HTTP servers include the following:

Windows options, such as Internet Information Services (IIS)
Linux options, such as Apache HTTP Server, Nginx, and Apache Tomcat
To run an HTTP server on AWS, you must find a service that provides compute power in the AWS Management Console. You can view the complete list of AWS compute services when you log in to the console.

To run an HTTP server on AWS, you must find a service that provides compute power in the AWS Management Console. You can view the complete list of AWS compute services when you log in to the console.

Choosing the right compute option

If you’re responsible for setting up servers on AWS to run your infrastructure, you have many compute options. First, you need to know which compute service to use for each use case. At a fundamental level, three types of compute options are available: virtual machines (VMs instanmces), container services, and serverless.
https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720936800/AXq6iF0MGvKt5w_wALPgYw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/VWfXPPKydiEKwe0c_RnozzfcimAtzGYe6.png

If you have prior infrastructure knowledge, a virtual machine will often be the easiest compute option to understand. This is because a virtual machine emulates a physical server and allows you to install an HTTP server to run your applications, for example. To run virtual machines, you install a hypervisor on a host machine. In its simplest form, a hypervisor is software or firmware that makes it possible to share physical hardware resources across one or more virtual machines. The hypervisor provisions the resources to create and run your VMs.

In AWS, Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure and resizable compute capacity in the cloud. You can provision virtual servers called EC2 instances. Behind the scenes, AWS operates and manages the host machines and the hypervisor layer. AWS also installs the virtual machine operating system, called the guest operating system.



Amazon EC2

Amazon EC2 is a web service that provides secure, resizable compute capacity in the cloud. With this service, you can provision virtual servers called EC2 instances. 

Amazon EC2 icon.
Amazon Elastic Compute Cloud (Amazon EC2)

With Amazon EC2, you can do the following:

Provision and launch one or more EC2 instances in minutes.
Stop or shut down EC2 instances when you finish running a workload.
Pay by the hour or second for each instance type (minimum of 60 seconds).
You can create and manage EC2 instances through the AWS Management Console, AWS CLI, AWS SDKs, automation tools, and infrastructure orchestration services.

To create an EC2 instance, you must define the following:


bullet
Hardware specifications: CPU, memory, network, and storage


bullet
Logical configurations: Networking location, firewall rules, authentication, and the operating system of your choice


Amazon Machine Image

When launching an EC2 instance, the first setting you configure is which operating system you want by selecting an Amazon Machine Image (AMI).

In the traditional infrastructure world, spinning up a server consists of installing an operating system from installation disks, drives, or wizards over the network. In the AWS Cloud, the operating system installation is not your responsibility. Instead, it's built into the AMI that you choose.

An AMI includes the operating system, storage mapping, architecture type, launch permissions, and any additional preinstalled software applications.

Relationship between AMIs and EC2 instances

EC2 instances are live instantiations (or versions) of what is defined in an AMI, as a cake is a live instantiation of a cake recipe. If you are familiar with software development, you can also see this kind of relationship between a class and an object. In this case, the AMI is how you model and define your instance. The EC2 instance is the entity you interact with, where you can install your web server and serve your content to users.

When you launch a new instance, AWS allocates a virtual machine that runs on a hypervisor. Then the AMI that you selected is copied to the root device volume, which contains the image that is used to boot the volume. In the end, you get a server that you can connect to and install packages and additional software on. In the example, you install a web server along with the properly configured source code of your employee directory application.

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720936800/AXq6iF0MGvKt5w_wALPgYw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/1-QE4YBuY5oLlkGT_b1oUsgei4V-I5ioF.png

One advantage of using AMIs is that they are reusable. You might choose a Linux-based AMI and configure the HTTP server, application packages, and additional software that you need to run your application. If you want to create another EC2 instance with the same configurations, you could create and configure a new EC2 instance to match the first instance. Or you could create an AMI from your running instance and use the AMI to start a new instance. That way, your new instance would have the same configurations as your current instance because the configurations set in the AMIs are the same.

An AMI includes the operating system, storage mapping, architecture type, launch permissions, and any additional preinstalled software applications.

Each AMI in the AWS Management Console has an AMI ID, which is prefixed by ami-, followed by a random hash of numbers and letters. The IDs are unique to each AWS Region.

Configuring EC2
EC2 instances are a combination of virtual processors (vCPUs), memory, network, and, in some cases, instance storage and graphics processing units (GPUs). When you create an EC2 instance, you need to choose how much you need of each of these components.e.

AWS offers a variety of instances that differ based on performance. Some instances provide more capacity than others. To get an overview of the capacity details for a particular instance, you should look at the instance type. Instance types consist of a prefix identifying the type of workloads they’re optimized for, followed by a size. For example, the instance type c5n.xlarge can be broken down as follows:

First position – The first position, c, indicates the instance family. This indicates that this instance belongs to the compute optimized family.
Second position – The second position, 5, indicates the generation of the instance. This instance belongs to the fifth generation of instances.
Remaining letters before the period – In this case, n indicates additional attributes, such as local NVMe storage.
After the period – After the period, xlarge indicates the instance size. In this example, it's xlarge.

EC2 instance locations

Unless otherwise specified, when you launch EC2 instances, they are placed in a default virtual private cloud (VPC). The default VPC is suitable for getting started quickly and launching public EC2 instances without having to create and configure your own VPC.

Any resource that you put inside the default VPC will be public and accessible by the internet, so you shouldn’t place any customer data or private information in it.

When you get more comfortable with networking on AWS, you should change this default setting to choose your own custom VPCs and restrict access with additional routing and connectivity mechanisms.

Architecting for high availability

In the network, your instance resides in an Availability Zone of your choice. As you learned previously, AWS services that are scoped at the Availability Zone level must be architected with high availability in mind.

Although EC2 instances are typically reliable, two are better than one, and three are better than two. Specifying the instance size gives you an advantage when designing your architecture because you can use more smaller instances rather than a few larger ones.

If your frontend only has a single instance and the instance fails, your application goes down. Alternatively, if your workload is distributed across 10 instances and one fails, you lose only 10 percent of your fleet, and your application availability is hardly affected.

When architecting any application for high availability, consider using at least two EC2 instances in two separate Availability Zones. 

EC2 instance lifecycle

An EC2 instance transitions between different states from the moment you create it until its termination.

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720936800/AXq6iF0MGvKt5w_wALPgYw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Xiqo31wijGzxUHcs_W-vfLyAzzrKyOEwn.png

When you launch an instance, it enters the pending state. When an instance is pending, billing has not started. At this stage, the instance is preparing to enter the running state. Pending is where AWS performs all actions needed to set up an instance, such as copying the AMI content to the root device and allocating the necessary networking components.


When your instance is running, it's ready to use. This is also the stage where billing begins. As soon as an instance is running, you can take other actions on the instance, such as reboot, terminate, stop, and stop-hibernate.


When you reboot an instance, it’s different than performing a stop action and then a start action. Rebooting an instance is equivalent to rebooting an operating system. The instance keeps its public DNS name (IPv4) and private and public IPv4 addresses. An IPv6 address (if applicable) remains on the same host computer and maintains its public and private IP address, in addition to any data on its instance store volumes.


When you stop your instance, it enters the stopping and then stopped state. This is similar to when you shut down your laptop. You can stop and start an instance if it has an Amazon Elastic Block Store (Amazon EBS) volume as its root device. When you stop and start an instance, your instance can be placed on a new underlying physical server. Your instance retains its private IPv4 addresses and if your instance has an IPv6 address, it retains its IPv6 address. When you put the instance into stop-hibernate, the instance enters the stopped state, but saves the last information or content into memory, so that the start process is faster.


When you terminate an instance, the instance stores are erased, and you lose both the public IP address and private IP address of the machine. Termination of an instance means that you can no longer access the machine. As soon as the status of an instance changes to shutting down or terminated, you stop incurring charges for that instance.

Difference between stop and stop-hibernate

When you stop an instance, it enters the stopping state until it reaches the stopped state. AWS does not charge usage or data transfer fees for your instance after you stop it. But storage for any Amazon EBS volumes is still charged. While your instance is in the stopped state, you can modify some attributes, like the instance type. When you stop your instance, the data from the instance memory (RAM) is lost.

When you stop-hibernate an instance, Amazon EC2 signals the operating system to perform hibernation (suspend-to-disk), which saves the contents from the instance memory (RAM) to the EBS root volume. You can hibernate an instance only if hibernation is turned on and the instance meets the hibernation prerequisites.

Container Services
Containers can host a variety of different workloads, including web applications, lift and shift migrations, distributed applications, and streamlining of development, test, and production environments.

Containers

Although containers are often referred to as a new technology, the idea started in the 1970s with certain UNIX kernels (the central core of the operating system) having the ability to separate their processes through isolation. At the time, this was configured manually, making operations complex.

With the evolution of the open-source software community, containers evolved. Today, containers are used as a solution to problems of traditional compute, including the issue of getting software to run reliably when it moves from one compute environment to another.

A container is a standardized unit that packages your code and its dependencies. This package is designed to run reliably on any platform, because the container creates its own independent environment. With containers, workloads can be carried from one place to another, such as from development to production or from on-premises environments to the cloud.

An example of a containerization platform is Docker. Docker is a popular container runtime that simplifies the management of the entire operating system stack required for container isolation, including networking and storage. Docker helps customers create, package, deploy, and run containers.


Difference between VMs and containers
Containers share the same operating system and kernel as the host that they exist on. But virtual machines contain their own operating system. Each virtual machine must maintain a copy of an operating system, which results in a degree of wasted resources.

A container is more lightweight. Containers spin up quicker, almost instantly. This difference in startup time becomes instrumental when designing applications that must scale quickly during I/O bursts.

Containers can provide speed, but virtual machines offer the full strength of an operating system and more resources, like package installation, dedicated kernel, and more.
https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720936800/AXq6iF0MGvKt5w_wALPgYw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/1iikq77Axc3_R0px_aLZuLt2uEP1sRZeR.png

Orchestrating containers

In AWS, containers can run on EC2 instances. For example, you might have a large instance and run a few containers on that instance. Although running one instance is uncomplicated to manage, it lacks high availability and scalability. Most companies and organizations run many containers on many EC2 instances across several Availability Zones.

If you’re trying to manage your compute at a large scale, you should consider the following:


bullet
How to place your containers on your instances


bullet
What happens if your container fails


bullet
What happens if your instance fails


bullet
How to monitor deployments of your containers

This coordination is handled by a container orchestration service. AWS offers two container orchestration services: Amazon Elastic Container Service (Amazon ECS) and Amazon Elastic Kubernetes Service (Amazon EKS).


Managing containers with Amazon ECS

Amazon ECS is an end-to-end container orchestration service that helps you spin up new containers. With Amazon ECS, your containers are defined in a task definition that you use to run an individual task or a task within a service. You have the option to run your tasks and services on a serverless infrastructure that's managed by another AWS service called AWS Fargate. Alternatively, for more control over your infrastructure, you can run your tasks and services on a cluster of EC2 instances that you manage.

https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1720936800/AXq6iF0MGvKt5w_wALPgYw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/j7c1On-84HBvzs8I_fBTShP26hpLTwZKE.png

If you choose to have more control by running and managing your containers on a cluster of Amazon EC2 instances, you will also need to install the Amazon ECS container agent on your EC2 instances. Note that an EC2 instance with the container agent installed is often called a container instance. This container agent is open source and responsible for communicating to the Amazon ECS service about cluster management details. You can run the agent on both Linux and Windows AMIs.

When the Amazon ECS container instances are up and running, you can perform actions that include, but are not limited to, the following:

Launching and stopping containers
Getting cluster state
Scaling in and out
Scheduling the placement of containers across your cluster
Assigning permissions
Meeting availability requirements
To prepare your application to run on Amazon ECS, you create a task definition. The task definition is a text file, in JSON format, that describes one or more containers. A task definition is similar to a blueprint that describes the resources that you need to run a container, such as CPU, memory, ports, images, storage, and networking information.


Using Kubernetes with Amazon EKS

Amazon EKS icon.
Amazon Elastic Kubernetes Service (Amazon EKS)

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services. By bringing software development and operations together by design, Kubernetes created a rapidly growing ecosystem that is very popular and well established in the market.

If you already use Kubernetes, you can use Amazon EKS to orchestrate the workloads in the AWS Cloud. Amazon EKS is a managed service that you can use to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane or nodes. Amazon EKS is conceptually similar to Amazon ECS, but with the following differences:


bullet
In Amazon ECS, the machine that runs the containers is an EC2 instance that has an ECS agent installed and configured to run and manage your containers. This instance is called a container instance. In Amazon EKS, the machine that runs the containers is called a worker node or Kubernetes node. 


bullet
An ECS container is called a task. An EKS container is called a pod.


bullet
Amazon ECS runs on AWS native technology. Amazon EKS runs on Kubernetes. 

If you have containers running on Kubernetes and want an advanced orchestration solution that can provide simplicity, high availability, and fine-grained control over your infrastructure, Amazon EKS could be the tool for you.

Introduction to Serverless
 If you want to deploy your workloads and applications without having to manage any EC2 instances, you can do that on AWS with serverless compute.

Go serverless


With serverless compute, you can spend time on the things that differentiate your application, rather than spending time on ensuring availability, scaling, and managing servers. Every definition of serverless mentions the following four aspects:

There are no servers to provision or manage.
It scales with usage.
You never pay for idle resources.
Availability and fault tolerance are built in.
AWS has developed serverless services for all three layers of the application stack.

Exploring serverless containers with AWS Fargate

Fargate abstracts the EC2 instance so that you’re not required to manage the underlying compute infrastructure. However, with Fargate, you can use all the same Amazon ECS concepts, APIs, and AWS integrations. It natively integrates with IAM and Amazon Virtual Private Cloud (Amazon VPC). With native integration with Amazon VPC, you can launch Fargate containers inside your network and control connectivity to your applications.


Running code on AWS Lambda

If you want to deploy your workloads and applications without having to manage any EC2 instances or containers, you can use Lambda.

AWS Lambda icon.
AWS Lambda

With Lambda, you can run code without provisioning or managing servers. You can run code for virtually any type of application or backend service. This includes data processing, real-time stream processing, machine learning, WebSockets, IoT backends, mobile backends, and web applications like your employee directory application!

Lambda runs your code on a high availability compute infrastructure and requires no administration from the user. You upload your source code in one of the languages that Lambda supports, and Lambda takes care of everything required to run and scale your code with high availability. There are no servers to manage. You get continuous scaling with subsecond metering and consistent performance.

How Lambda works

The Lambda function is the foundational principle of AWS Lambda. You have the option of configuring your Lambda functions using the Lambda console, Lambda API, AWS CloudFormation, or AWS Serverless Application Model (AWS SAM). You can invoke your function directly by using the Lambda API, or you can configure an AWS service or resource to invoke your function in response to an event.


A function is a resource that you can invoke to run your code in Lambda. Lambda runs instances of your function to process events. When you create the Lambda function, it can be authored in several ways:

You can create the function from scratch.
You can use a blueprint that AWS provides.
You can select a container image to deploy for your function.
You can browse the AWS Serverless Application Repository. 


Triggers describe when a Lambda function should run. A trigger integrates your Lambda function with other AWS services and event source mappings. So you can run your Lambda function in response to certain API calls or by reading items from a stream or queue. This increases your ability to respond to events in your console without having to perform manual actions. 


An event is a JSON-formatted document that contains data for a Lambda function to process. The runtime converts the event to an object and passes it to your function code. When you invoke a function, you determine the structure and contents of the event.

An application environment provides a secure and isolated runtime environment for your Lambda function. An application environment manages the processes and resources that are required to run the function. 

You deploy your Lambda function code using a deployment package. Lambda supports two types of deployment packages:

                   

A .zip file archive – This contains your function code and its dependencies. Lambda provides the operating system and runtime for your function.

A container image – This is compatible with the Open Container Initiative (OCI) specification. You add your function code and dependencies to the image. You must also include the operating system and a Lambda runtime.





The runtime provides a language-specific environment that runs in an application environment. When you create your Lambda function, you specify the runtime that you want your code to run in. You can use built-in runtimes, such as Python, Node.js, Ruby, Go, Java, or .NET Core. Or you can implement your Lambda functions to run on a custom runtime.


The AWS Lambda function handler is the method in your function code that processes events. When your function is invoked, Lambda runs the handler method. When the handler exits or returns a response, it becomes available to handle another event. 



You can use the following general syntax when creating a function handler in Python.



def handler_name (event, context):

...

return some_value






















































Refereences
Compute services: https://docs.aws.amazon.com/whitepapers/latest/aws-overview/compute-services.html

Compute Services
https://aws.amazon.com/products/compute/


Default VPCs:
https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html

How Amazon VPC works:
https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html

Instance lifecycle:
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html

Containers on AWS: https://aws.amazon.com/containers/services/
What is a cointainer: 
https://www.docker.com/resources/what-container/

Amazon Elastic Container Service:
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-capacity.html

What is Amazon EKS?
https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html


Serverless on AWS:
https://aws.amazon.com/serverless/#:~:text=Serverless%20is%20the%20native%20architecture,services%20without%20thinking%20about%20servers.

Configuring AWS Lambda functions:
https://docs.aws.amazon.com/lambda/latest/dg/lambda-functions.html
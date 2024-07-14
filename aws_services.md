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


Refereences
Compute services: https://docs.aws.amazon.com/whitepapers/latest/aws-overview/compute-services.html

Compute Services
https://aws.amazon.com/products/compute/




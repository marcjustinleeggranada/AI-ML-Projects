<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-ec2)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Launching VPC Resources

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you launch AWS resources in a logically isolated virtual network that you define, and it is useful because it gives you complete control over your virtual networking environment, including selecting your own IP address ranges, creating subnets, and configuring route tables and security groups to securely isolate and protect backend resources from direct internet access.

### How I used Amazon VPC in this project

I used Amazon VPC to design and launch an isolated virtual network featuring both public and private environments. This setup allowed me to deploy a public EC2 instance to route internet traffic and a private backend server protected by custom security groups and route tables to secure sensitive data.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how incredibly fast and visual the process of building an entire network could be when using the VPC wizard in the AWS Management Console. Seeing the dynamic resource map automatically link subnets, route tables, and the internet gateway in real time made the relationships between these complex networking components much easier to understand than setting them up manually.

### This project took me...

This project took me about 60 minutes to complete. During this time, I successfully configured my network infrastructure, launched both public and private EC2 instances, and learned how to dynamically provision an isolated network setup in minutes using the Amazon VPC wizard.

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means logging into and managing its operating system or software over the internet as if the physical hardware were right in front of you. Unlike using the AWS Management Console for high-level resource administration, direct access lets you open a terminal, run commands, install custom software, and modify configuration files directly on your EC2 instance.

### SSH is a key method for directly accessing a VM

SSH traffic (Secure Shell) means secure, encrypted communication sent over a network on port 22 to enable remote system administration. It is primarily used to securely log into and run commands on virtual servers, such as EC2 instances, ensuring that sensitive authentication credentials and command data are protected from interceptors while traveling across the internet.

### To enable direct access, I set up key pairs

Key pairs are secure authentication tools consisting of a public key installed on EC2 instances and a corresponding private key held by the user. They work together using cryptographic keys to verify your identity and grant direct, secure administrative access to your virtual machines over the internet without needing a traditional password.

A private key's file format means the specific structure and encoding used to store cryptographic credentials so they can be parsed by compatible systems. My private key's file format was .pem (Privacy Enhanced Mail), which is the highly compatible industry-standard format used to manage credentials for securely connecting to EC2 instances.

---

## Launching a public server

I had to change my EC2 instance's networking settings by selecting my custom VPC, placing the instance in a public subnet, and enabling the Auto-assign public IP setting. This configuration ensures that the EC2 instance receives a reachable public IPv4 address, which is a key requirement for using EC2 Instance Connect to successfully establish a secure connection to the server.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because it requires highly restrictive access controls that differ from a public-facing resource. While my public server must accept general web traffic from the internet, my private server contains sensitive backend resources that must be isolated. Having a unique security group allows me to block all direct public access and limit inbound SSH traffic exclusively to trusted resources within my VPC, such as my public EC2 instance.

My private server's security group's source is the NextWork Public Security Group, which means only resources associated with that specific public security group can communicate with my private instance. This configuration blocks all direct inbound SSH traffic from the public internet (0.0.0.0/0) and limits access exclusively to trusted resources within my VPC.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I leveraged the VPC wizard by selecting the "VPC and more" option in the AWS Management Console. This allowed me to automatically provision my entire networking infrastructure—including public and private subnets, an internet gateway, and route tables—all at once, while using the interactive resource map to immediately visualize how these resources connect.

A VPC resource map is an interactive, visual tool within the AWS Management Console that dynamically displays the layout and connections within a VPC. It shows relationships between subnets, route tables, and network connections like an internet gateway, allowing developers to design, manage, and troubleshoot their cloud infrastructure at a glance.

My new VPC has a CIDR block of 10.0.0.0/16. It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because AWS VPCs are logically isolated networks by default, meaning they do not share internal routing tables or cause address conflicts unless you explicitly connect them through VPC peering.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: 0 or 2. This was because the VPC wizard enforces AWS best practices for high availability and redundancy. Since I selected two Availability Zones, the wizard ensures that a public subnet is deployed in each zone, protecting my public resources from being entirely offline if a single zone experiences an outage.

NAT gateways are network address translation services that allow resources in a private subnet to connect outbound to the internet for software updates and patches, while blocking unauthorized inbound connections. They differ from internet gateways, which allow bidirectional (both inbound and outbound) communication for resources residing in public subnets.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-ec2_8ee57662)

---

---

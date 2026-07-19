<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-peering)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## VPC Peering

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you provision a logically isolated virtual network within the AWS Cloud. It is useful because it gives you complete control over your cloud environment, allowing you to customize features like subnets, route tables, and security groups to isolate and protect your resources from unauthorized public internet access.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to provision two separate, isolated virtual networks with unique CIDR blocks and connected them using a VPC peering connection. I then updated the route tables for both networks to route cross-VPC traffic and modified security groups to permit ICMP traffic, enabling secure, private communication between my EC2 instances without sending data over the public internet.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that establishing a VPC peering connection doesn't automatically enable traffic flow. I was surprised that I had to manually configure reciprocal paths in the route tables for both networks and explicitly allow ICMP traffic in the destination security groups before a simple ping command would succeed.

### This project took me...

This project took me about 60 minutes to complete, as it was highly rewarding to configure the VPC peering connection, update both route tables, and troubleshoot the security group rules until my EC2 instances could successfully send and receive private ICMP traffic.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will create two separate VPCs using the visual VPC wizard because establishing isolated networks with unique IPv4 CIDR blocks is required before we can build and validate a private VPC Peering connection between them.

### Step 2 - Create a Peering Connection

In this step, I will create a VPC Peering connection between NextWork-1-VPC and NextWork-2-VPC because we need to establish a secure, private communication link that allows resources in both networks to route traffic directly using private IP addresses instead of exposing our data to the public internet.

### Step 3 - Update Route Tables

In this step, I will configure the route tables for both VPCs to point toward our newly created peering connection because establishing the connection itself does not automatically route traffic; we must explicitly instruct each network how to reach the other's unique CIDR block.

### Step 4 - Launch EC2 Instances

In this step, I will launch an EC2 instance in each VPC because we need active compute resources in both networks to generate traffic and validate that our VPC peering connection is successfully routing private data between them.

---

## Multi-VPC Architecture

I started my project by launching two separate VPCs named NextWork-1 and NextWork-2 using the visual VPC wizard in the AWS Management Console. This allowed me to quickly spin up the necessary network infrastructure, including subnets and route tables, which serves as the foundation for setting up our VPC Peering connection.

The CIDR blocks for VPC 1 and VPC 2 are 10.1.0.0/16 and 10.2.0.0/16 respectively. They have to be unique because if their IPv4 CIDR blocks overlap, AWS cannot properly route traffic between them. This uniqueness is critical when setting up a VPC Peering connection, as overlapping IP address ranges would cause routing conflicts and prevent resources in separate VPCs from communicating privately.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as we are using EC2 Instance Connect to access them, meaning AWS dynamically manages the SSH key pairs for us behind the scenes. This allows us to connect securely directly from our web browser without the administrative overhead of manually creating and managing local private key files.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a secure networking connection established between two separate VPCs that enables them to route traffic directly and privately. By bridging these virtual networks, resources in both VPCs can communicate with each other using private IP addresses as if they were on the same local network, completely bypassing the public internet to ensure maximum security and low latency.

VPCs would use peering connections to privately share databases and internal services across different development teams, facilitate secure data transfers between business units, and connect multi-tier application architectures without exposing critical resources. By routing traffic through these connections, resources can communicate directly using private IP addresses, keeping sensitive data completely off the public internet.

The difference between a Requester and an Accepter in a VPC Peering connection is that the Requester is the VPC that initiates the connection by sending an invitation, whereas the Accepter is the receiving VPC that must approve the invitation before the direct, private communication link is established.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated becaAfter accepting a peering connection, my VPCs' route tables need to be updated because establishing the peering link only creates the pathway between the networks; it does not automatically configure how traffic flows. We must explicitly add a static route in each VPC's route table that maps the destination CIDR block of the peered network to the VPC Peering connection target. Without these routing rules, resources in separate VPCs will not know how to locate each other, and all inter-VPC traffic will be dropped.use...

My VPCs' new routes have a destination of 10.2.0.0/16 for NextWork-1's route table (targeting VPC 2) and 10.1.0.0/16 for NextWork-2's route table (targeting VPC 1). The routes' target was our active VPC Peering connection, named VPC 1 <> VPC 2, ensuring traffic between the two virtual networks is routed directly and securely.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 Instance Connect to connect to my first EC2 instance and troubleshoot the resulting connection failure because the instance was launched without a public IPv4 address. Resolving this by allocating and associating an Elastic IP address will teach me how to establish secure, internet-based management access to instances hosted within a public subnet.

### Step 6 - Connect to EC2 Instance 1

In this step, I will attempt to connect to my EC2 instance again using EC2 Instance Connect and troubleshoot a new connection failure by editing its security group inbound rules. I am doing this because the default security group blocks all incoming traffic from outside the VPC by default, and we must explicitly allow inbound SSH traffic on port 22 to allow the service to connect over the internet.

### Step 7 - Test VPC Peering

In this step, I will run the ping command from Instance 1 to Instance 2 using its private IP address because we need to test if our VPC peering connection is working and troubleshoot any network security or routing blocks until both servers can communicate.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to securely log into my first EC2 instance directly from the browser because it eliminates the need to manually manage local key pairs. Since AWS dynamically handles SSH credentials behind the scenes, this approach allows me to quickly establish an SSH connection to troubleshoot and manage my resources with enhanced convenience and security.

I was stopped from using EC2 Instance Connect as my EC2 instance did not have a public IPv4 address assigned to it. Because EC2 Instance Connect communicates with the server over the public internet, the connection failed because we kept the auto-assign IP option disabled during the instance launch, leaving the instance with only a private IP address inside our subnet.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static, public IPv4 addresses allocated to your AWS account that can be dynamically associated with any EC2 instance. Unlike default dynamic IP addresses that change whenever an instance is restarted, an Elastic IP address remains permanent, providing a reliable and persistent network address that allows us to successfully connect to our server using EC2 Instance Connect.

Associating an Elastic IP address resolved the error because EC2 Instance Connect communicates with the server over the public internet, which requires the target machine to have a routeable public endpoint. Since our EC2 instance was initially launched with only a private IP address, provisioning and attaching this static, public IPv4 address provided the necessary internet pathway for AWS to establish a successful SSH connection.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the ping command followed by the target server's private IP address, specifically entering ping 10.2.15.117 within the terminal of my first EC2 instance to send test packets across the VPC peering connection.

A successful ping test would validate my VPC peering connection because it proves that bi-directional routing is correctly configured in both route tables to direct private traffic through the peering connection, and that the firewalls, such as Security Groups and Network ACLs, are successfully allowing ICMP traffic to pass between the peered subnets without routing over the public internet.

I had to update my second EC2 instance's security group because the default security group blocks all inbound ICMP traffic by default, which prevented the ping command sent from Instance 1 from reaching it. I added a new rule that allowed All ICMP - IPv4 traffic from the source 10.1.0.0/16, which successfully let the diagnostic packets pass through the firewall and return successful replies.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-peering_7a29d352)

---

---

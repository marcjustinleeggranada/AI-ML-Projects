<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-security)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a private, isolated section of the AWS Cloud where you can safely run your resources, and it is useful because it gives you complete control over your network environment, allowing you to secure your data by customizing subnets, configuring route tables, and creating layered firewalls like security groups and network ACLs.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to build a secure network environment by configuring a custom route table to guide outbound traffic, setting up a security group to filter resource-level connections, and deploying a network ACL to provide a stateless layer of defense for my subnets.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that a custom network ACL is completely stateless and automatically denies all inbound and outbound traffic upon creation. I expected it to behave like a security group which allows outbound traffic by default, so learning that I had to explicitly configure rules for both traffic directions to establish subnet-level security was an unexpected but valuable lesson in layered network defense.

### This project took me...

This project took me about 45 minutes to complete because configuring the different security layers—including Amazon VPC route tables, resource-level security groups, and subnet-level network ACLs—required careful attention to detail, but following the step-by-step instructions allowed me to complete the setup and understand traffic flows smoothly.

---

## Route tables

Route tables are collections of routing rules, called routes, that act like a GPS for your network resources by determining where network traffic from your subnet or gateway is directed. Every subnet in an Amazon VPC must be associated with a route table, which maps destination IP addresses to specific targets, such as an internet gateway for external communication or local for internal traffic.

Route tables are needed to make a subnet public because they contain the routing rules that direct traffic. Specifically, to make a subnet public, its associated route table must have a route that directs internet-bound traffic (0.0.0.0/0) to an attached internet gateway. Without this rule, resources inside the subnet will have no path to send or receive data from the public internet.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which mean the destination is the specific range of IP addresses that network traffic is trying to reach, while the target is the gateway, connection, or resource that the traffic is directed through to get there, such as using local for internal communication within an Amazon VPC or an internet gateway to reach the public internet.

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 and a target of my internet gateway ID, such as igw-05e9d23d4d2f0e725 (specifically my NextWork IG). This setup ensures that any outbound traffic not meant for internal communication within my Amazon VPC is correctly forwarded to the public internet.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are virtual firewalls that operate at the resource level within an Amazon VPC, acting like a security checkpoint at the entrance of individual resources. Unlike network access control lists that apply broadly to subnets, a security group attaches directly to a specific resource to secure it by controlling inbound and outbound traffic based on defined protocols, port numbers, and IP addresses.

### Inbound vs Outbound rules

Inbound rules are security group settings that define what incoming traffic is permitted to reach your network resources based on specific protocols, ports, and source IP addresses. I configured an inbound rule that allows HTTP traffic over Port 80 from Anywhere-IPv4 (0.0.0.0/0) to ensure that public visitors on the internet can successfully reach and view the website hosted on my resource.

Outbound rules are security configurations that determine what network traffic is allowed to leave the resources associated with a security group. By default, my security group's outbound rule is set to allow all outgoing traffic to any destination on the internet (0.0.0.0/0), which ensures that my resources can freely initiate connections and send data external to the network without being blocked.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs (Network Access Control Lists) are subnet-level virtual firewalls that control inbound and outbound traffic for your subnets. They act like security checkpoints at the boundary of each subnet, inspecting incoming and outgoing data packets against a numbered list of rules to determine whether they should be allowed or denied before they can ever reach your resources within an Amazon VPC.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that a security group acts as a stateful firewall operating at the individual resource level, automatically allowing return traffic. In contrast, a network ACL acts as a stateless firewall operating at the subnet level, requiring you to configure explicit rules for both inbound and outbound traffic directions.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a default network ACL's inbound and outbound rules will automatically allow all incoming and outgoing traffic into and out of your subnets, whereas any custom network ACL you create will deny all traffic until you explicitly add rules to permit it.

In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all traffic. This secure-by-default behavior ensures that your subnet is completely protected from any incoming or outgoing data packets until you explicitly configure rules in your custom network ACL to allow specific traffic.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

---

---

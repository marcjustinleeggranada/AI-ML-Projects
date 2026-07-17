<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-connectivity)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Testing VPC Connectivity

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

An Amazon VPC is a logically isolated virtual network within the AWS Cloud that allows you to provision and manage your own private section of the cloud infrastructure. It is useful because it gives you absolute control over your network environment, enabling you to define IP address ranges, create public and private subnets, configure route tables, and implement robust security boundaries using security groups and Network ACLs to protect your backend resources from unauthorized internet access.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to provision a secure, multi-tier network by establishing both public and private subnets to isolate my EC2 instances. By defining rules in route tables and managing traffic filters with stateful security groups and stateless Network ACLs, I successfully validated secure internal communication between my servers and established outbound internet access through an Internet Gateway.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how a silent block in a stateless Network ACL could completely stop a curl command from working. I didn't realize that even with outbound internet access and security groups configured correctly, returning traffic on ephemeral ports and DNS resolution queries over UDP Port 53 would be quietly dropped by the subnet boundary unless explicitly permitted. Troubleshooting this highlighted the critical difference between stateful and stateless firewalls within an Amazon VPC.

### This project took me...

This project took me approximately 60 minutes of active hands-on work to complete, finishing my final tests at 2:30 PM UTC. While setting up the Amazon VPC infrastructure and launching the EC2 instances went smoothly, I spent the majority of my time troubleshooting and understanding how stateless Network ACLs filter inbound and outbound traffic during my curl tests.

---

## Connecting to an EC2 Instance

Connectivity refers to the ability of different resources within a network, such as EC2 instances in public and private subnets, to securely communicate and exchange data with each other and with external networks like the internet. In Amazon VPC, establishing connectivity depends on defining path rules in route tables and managing traffic permission boundaries using security groups and Network ACLs.

My first connectivity test was whether I could connect to my Public Server using EC2 Instance Connect from the AWS Management Console. This initial test served to verify that public-facing internet routes through the Internet Gateway were properly established and that my public subnet settings allowed traffic to reach the instance.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is a browser-based SSH tool that allows me to securely connect to my EC2 instances directly through the AWS Management Console. It simplifies the connection process by dynamically managing temporary SSH keys on my behalf, eliminating the need to manually generate, store, or configure private key files on my local machine.

My first attempt at getting direct access to my public server resulted in an error because the public subnet's route table did not have a route directing traffic to the Internet Gateway, which meant there was no path to the internet. Additionally, the instance's security group lacked an inbound rule allowing SSH traffic on Port 22 from the internet, causing the connection request from EC2 Instance Connect to time out.

I fixed this error by updating my public subnet's route table to include a route for 0.0.0.0/0 pointing to the Internet Gateway, establishing a path to the outside world. Additionally, I edited the security group attached to my EC2 instance by adding an inbound rule that explicitly allows SSH traffic on Port 22 from 0.0.0.0/0, which enabled EC2 Instance Connect to successfully authenticate and open the terminal.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a network utility tool used to check whether a device can communicate with another device on a network and to measure how long it takes for a data packet to make the round trip. I used ping to test the connectivity between my Public Server and my Private Server inside the VPC. This test validated whether ICMP traffic was permitted to flow between the two subnets by evaluating if our security groups and Network ACLs were correctly configured to allow communication.

The ping command I ran was ping The ping command I ran was ping 10.0.1.248 (using the target server's specific private IP address). I ran this command from the terminal of my public server to send ICMP network packets directly to my second EC2 instance, allowing me to test whether a direct network path was open between them.(using the target server's specific private IP address). I ran this command from the terminal of my public server to send ICMP network packets directly to my second EC2 instance, allowing me to test whether a direct network path was open between them.

The first ping returnedPING 10.0.1.248 (10.0.1.248) 56(84) bytes of data. This meant...

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

This output meant that my public server successfully initiated the ping command and resolved the target IP address, but it did not receive any subsequent reply lines from the destination. This hang indicates that while a connection request was sent, the traffic was dropped before a reply could return, pointing to a block on ICMP traffic by either the destination's security group or the associated Network ACL.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a command-line tool used to transfer data to or from a server over various network protocols. While utilities like ping only check basic reachability, curl allows you to send HTTP and HTTPS requests to retrieve raw resource files, such as HTML code, from web servers across the public internet.

I used curl to test the connectivity between my Public Server and the external internet. By successfully retrieving the raw HTML content of public web pages like example.com, I verified that my public subnet had a working outbound path through the Internet Gateway and that my Network ACL and security groups were configured correctly to allow traffic to flow both ways.

### Ping vs Curl

Ping and curl are different because ping uses the ICMP protocol to test basic server reachability and network latency without fetching any data, whereas curl uses application-layer protocols like HTTP or HTTPS to actually transfer and download raw web page content from a target server.

---

## Connectivity to the Internet

I ran the curl command curl example.com, which returned the complete, raw HTML code for the website's landing page. This response, containing structural web tags like <!doctype html> and body sections, validated that our VPC's routing, security groups, and stateless Network ACLs were perfectly configured to allow outbound HTTP/HTTPS requests and accept their returning responses.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-connectivity_8ee57662)

---

---

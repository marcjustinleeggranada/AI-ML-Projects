<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://nextwork.ai/projects/aws-networks-s3)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Access S3 from a VPC

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you launch AWS resources in a logically isolated virtual network that you define. It is useful because it gives you complete control over your virtual networking environment, including selecting your own IP address range, creating subnets, and configuring route tables and network gateways, allowing you to secure your application architecture and control how your EC2 instances communicate with other AWS services.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to provision a logically isolated virtual network with a public subnet and launch an EC2 instance inside it. By setting up IAM access keys and running AWS CLI commands directly from my server's terminal, I established a secure baseline configuration that allowed my instance to cross the VPC boundary and interact with files stored in my Amazon S3 bucket.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was realizing that even though my EC2 instance and Amazon S3 bucket are in the same AWS account, they cannot communicate by default because S3 lives outside the boundaries of a VPC. I expected some form of automatic internal access, so discovering that I had to explicitly configure IAM access keys to bridge this gap really highlighted how isolated resources inside a virtual network are from public AWS services.

### This project took me...

This project took me approximately 60 minutes to complete from start to finish. Most of my time was spent setting up the custom Amazon VPC, configuring the access keys on my EC2 instance, and running AWS CLI commands to verify connectivity to Amazon S3, which was incredibly satisfying once the file copy successfully completed.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will create a custom Amazon VPC and launch an EC2 instance within its public subnet because these resources provide the foundational network isolation and virtual compute power required to host our environment and perform command-line tasks in later steps.

### Step 2 - Connect to my EC2 instance

In this step, I will connect directly to my EC2 instance using EC2 Instance Connect because accessing the server's terminal is necessary to test our initial connectivity and run AWS CLI commands, letting us observe how the instance interacts with other AWS services like Amazon S3 before we have access keys configured.

### Step 3 - Set up access keys

In this step, I will generate IAM access keys and configure them on my EC2 instance because these credentials provide the programmatic permissions needed for the AWS CLI to securely authenticate and interact with other services like Amazon S3.

---

## Architecture set up

I started my project by launching a custom Amazon VPC with a single public subnet using the VPC and more wizard option, making sure to disable costly NAT gateways. Inside this newly provisioned network, I launched an EC2 instance configured with an auto-assigned public IP address and a secure key pair, providing me with a stable and accessible host to run command-line tools in the upcoming steps.

I also set up a globally unique Amazon S3 bucket named nextwork-vpc-project-marc within my active AWS region. To finish this step, I uploaded two test images from my local computer into this bucket, creating the storage resources needed to verify programmatic access from my EC2 instance using the AWS CLI in the next phase of the project.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

The AWS CLI is a unified command-line tool that allows users to control, manage, and automate AWS services directly through text-based commands in a terminal. I have access to the AWS CLI because it comes pre-installed by default on all Amazon Linux EC2 instances, allowing me to execute commands to interact with my AWS resources immediately upon connecting.

The first command I ran was aws s3 ls. This command is used to retrieve and display a list of all Amazon S3 buckets within my AWS account, allowing me to check if my session had the active network connection and valid IAM credentials required to interact with AWS services via the AWS CLI.

The second command I ran was aws configure. This command is used to securely initialize my local AWS CLI profile by prompting me for my Access Key ID, Secret Access Key, default region, and default output format. By saving these credentials on my EC2 instance, the terminal gains the necessary permissions to authenticate and execute commands against resources in my AWS account, such as my Amazon S3 bucket.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured my Access Key ID and Secret Access Key to securely authenticate my programmatic identity, specified my default AWS Region to route commands to the correct geographic location, and left the default output format blank to default to JSON, completing the entire setup using the aws configure command on the AWS CLI.

Access keys are long-term security credentials for an IAM user that consist of an Access Key ID and a Secret Access Key, which function like a programmatic username and password. They are used to authenticate and sign requests sent to AWS, allowing tools like the AWS CLI on an EC2 instance to securely connect to and manage services like Amazon S3.

Secret access keys are highly sensitive security credentials that work in tandem with an Access Key ID to cryptographically sign programmatic requests to AWS. Much like a password paired with a username, they verify the identity of an IAM user or application attempting to access resources. Because anyone who obtains a secret access key can gain full access to your AWS account, they must be kept strictly confidential, never committed to code, and downloaded only once during creation.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use an IAM role attached directly to the EC2 instance. This allows the server to automatically acquire temporary, self-rotating security credentials instead of hardcoding or storing long-term IAM access keys locally, which drastically improves security and simplifies credential management.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I will create a globally unique Amazon S3 bucket and upload two test files because establishing this storage resource is necessary to verify if my EC2 instance can successfully connect to and retrieve objects from Amazon S3 using the AWS CLI in the upcoming steps.

### Step 5 - Connecting to my S3 bucket

In this step, I will connect back to my EC2 instance terminal and configure the AWS CLI using my active IAM access keys because this allows me to authenticate my server and successfully list the objects inside my Amazon S3 bucket, verifying our programmatic network connection.

---

## Connecting to my S3 bucket

The first command I ran was aws s3 ls. This command is used to retrieve and display a list of all Amazon S3 buckets within my AWS account, allowing me to check if my session had the active network connection and valid IAM credentials required to interact with AWS services via the AWS CLI.

When I ran the command aws s3 ls again, the terminal responded with a list of the active buckets in my AWS account, including nextwork-vpc-project-marc. This indicated that the access keys I configured during setup were valid, allowing my EC2 instance to successfully authenticate and interact with Amazon S3 resources using the AWS CLI.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls s3://nextwork-vpc-project-marc, which returned the details of the objects stored inside my bucket, displaying the two uploaded images, mech1 and mech2. This output successfully demonstrated that my EC2 instance had the active network routing and authentic credentials needed to dive deep into my Amazon S3 bucket and read its contents.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/nextwork.txt. This command creates an empty text file named nextwork.txt inside the temporary /tmp/ directory of my EC2 instance using elevated superuser privileges, giving me a local file on the server's file system that is ready to be transferred to my Amazon S3 bucket using the AWS CLI in the next step.

The second command I ran was aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-project-marc. This command will copy the empty nextwork.txt file from the temporary directory of my EC2 instance and upload it directly into my globally unique Amazon S3 bucket, allowing me to verify outbound file transfer capabilities over the network using the AWS CLI.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-marc, which validated that my new test.txt file was successfully copied over and saved inside my Amazon S3 bucket. Seeing the file listed with a size of 0 bytes alongside my mech1 and mech2 images confirmed that the AWS CLI on my EC2 instance can successfully read the contents of the bucket and that my files are securely stored in the cloud.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-networks-s3_3e1e79a2)

---

---

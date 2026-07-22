<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://nextwork.ai/projects/aws-devops-vscode)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

## Set Up a Web App Using AWS and VS Code

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

In this project, I will demonstrate how to launch an Amazon EC2 instance and establish a remote SSH connection using VS Code. I am doing this project to learn how to configure development dependencies, specifically Java and Apache Maven, and deploy a basic Java web application in the cloud as the first step toward building a complete CI/CD pipeline.

This project is part one of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project tomorrow to connect my local code to a remote GitHub repository, establishing the secure version control foundation we need for automated deployments.

I did this project to learn DevOps engineering basics. By launching an Amazon EC2 instance, installing Java and Apache Maven, and connecting via VS Code Remote - SSH, I now have a solid cloud host ready for my CI/CD pipeline.

### Key tools and concepts

Services I used were Amazon EC2 to run my cloud server and AWS IAM to manage my administrator permissions. Key concepts I learnt include establishing secure remote SSH connections from my local VS Code workspace, modifying file permissions on Windows using icacls, configuring inbound firewall rules with security groups, and using Apache Maven alongside Amazon Corretto to automate building Java web application directory structures.

### Project reflection

This project took me approximately 2 hours. The most challenging part was troubleshooting the remote SSH connection timeout, which required me to modify my Windows private key permissions using icacls and temporarily adjust my security group rules to bypass my local network's changing IP address. It was most rewarding to successfully establish the connection using the VS Code Remote - SSH extension and see Apache Maven instantly generate our baseline Java web application files on the remote server.

One thing I didn't expect in this project was how dynamic IP allocation on my home network would affect my cloud setup. I was surprised to learn that restricting my security groups strictly to my own IP address would actually block the web-based EC2 Instance Connect tool, as those connection requests originate from AWS service servers rather than my local machine. Troubleshooting this connection timeout gave me a much deeper, practical understanding of how network firewalls and routing work.

---

## Launching an EC2 instance

### What I did in this step

In this step, I will launch an Amazon EC2 instance, configure its network settings, and create a new key pair because we need a secure, dedicated virtual server in the cloud to host our web application files and build our development environment.

I started this project by launching an Amazon EC2 instance because we need a reliable virtual server in the cloud to host our Java web application and set up our development tools, including Apache Maven, in an isolated and scalable environment.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_7852fbf3)

### I also enabled SSH

SSH is a secure, cryptographic network protocol used to establish an encrypted connection between a local computer and a remote server over an unsecured network. I enabled SSH so that I could securely connect my local machine and VS Code to my Amazon EC2 instance, allowing me to run terminal commands, manage files, and install development dependencies as if I were working directly on the remote server.

### Key pairs

A key pair is a secure method of authentication consisting of a public key that AWS stores on your instance and a matching private key that you download, which together verify your identity and grant safe remote access to your Amazon EC2 virtual server.

### Downloaded key pair file

Once I set up my key pair, AWS automatically downloaded a private key file with a .pem extension (named nextwork-keypair.pem) to my local computer. This sensitive file acts as the cryptographic credential that matches the public key stored on the cloud host, allowing me to securely authenticate and establish an SSH connection to my Amazon EC2 instance.

---

## Set up VS Code

### What I did in this step

In this step, I will download and install VS Code, open its integrated terminal, and modify the permissions of my key pair because we need a local development environment and a secure private key to establish a safe remote connection to our Amazon EC2 instance.

### What is VS Code?

VS Code is a powerful, lightweight Integrated Development Environment (IDE) that developers use to write, edit, and debug code. In this project, it acts as our main workspace, allowing us to manage our project files, edit our index.jsp web application code, and run terminal commands directly on our remote Amazon EC2 instance.

I installed VS Code to act as my primary IDE, allowing me to establish a secure SSH connection to my remote Amazon EC2 instance, write and edit my Java web app files, and run backend commands directly from a unified local workspace.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

A terminal is a text-based interface where you send instructions directly to your computer's operating system using text commands instead of clicking graphical menus. The first command I ran for this project is cd ~\Desktop\DevOps in PowerShell to navigate into my dedicated DevOps folder where my downloaded private key file is stored.

### Updating file permissions

I also updated my private key's permissions by running the icacls command in PowerShell, using the /inheritance:r parameter to strip away inherited parent folder permissions and the /grant:r parameter to restrict read-only access strictly to my own Windows user account, securing the private key for our SSH connection.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

### What I did in this step

In this step, I will establish a secure SSH connection to my Amazon EC2 instance using VS Code because we need to gain direct terminal access to our virtual server in order to install development dependencies and configure our web application within a unified remote workspace.

### Connecting to EC2

To connect to my EC2 instance, I ran the command ssh -i "C:\Users\Justin\Desktop\DevOps\nextwork-keypair.pem" ec2-user@ec2-13-250-29-29.ap-southeast-1.compute.amazonaws.com in my terminal because we need to use our secure private key file to authenticate our identity and establish an encrypted SSH connection directly to our remote virtual server.

### This command required an IPv4 address

A server's IPv4 DNS is a unique, human-readable domain name that maps directly to the server's numerical IPv4 address. In AWS, this hostname is automatically assigned to our Amazon EC2 instance, allowing tools like VS Code to easily locate and establish a secure SSH connection to the virtual server without us needing to memorize complex IP numbers.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

### What I did in this step

In this step, I will install Apache Maven and Amazon Corretto 8 on my Amazon EC2 instance, then verify their successful installations, because Java is a mandatory prerequisite for Maven to function, and having both tools ready will allow us to automate the building and scaffolding of our Java web application.

### Why I'm using Maven

Apache Maven is a comprehensive build automation and package manager tool designed specifically for Java software projects. We are using it in this project to automatically download external code dependencies and utilize pre-configured templates called archetypes to quickly generate the baseline structure of our web application.

Maven is required in this project because it serves as our build automation tool and package manager, allowing us to automatically scaffold a standard Java web application structure using a pre-configured template called an archetype. Without it, we would have to compile our code manually, organize project folders from scratch, and individually manage external libraries and dependencies, which would add significant manual overhead to our development workflow.

### Why I'm using Java

Java is a high-level, object-oriented programming language designed to be platform-independent, allowing developers to write code once and run it anywhere a Java Virtual Machine is installed. In this project, it serves as the foundational runtime environment for our web application and acts as a mandatory prerequisite that enables Apache Maven to successfully execute and build our project code.

Java is required in this project because it provides the foundational runtime environment needed to execute our web application on the Amazon EC2 instance. Additionally, Apache Maven, which we use to automate and build our project dependencies, is a Java-based tool that directly relies on the Java Virtual Machine to compile and package our application code.

---

## Create the Application

### What I did in this step

In this step, I will execute the Maven archetype command in my Amazon EC2 terminal to generate a new Java web application because using a pre-configured template allows us to automatically scaffold the entire project folder structure and start editing our code without manual setup.

### Creating the Java web app

I generated a Java web app using the command mvn archetype:generate with the maven-archetype-webapp template because it automatically scaffolds a standardized folder layout and sets up the foundational configuration files for a Java web application on our Amazon EC2 instance, allowing us to instantly begin developing without organizing the workspace manually.

### Installing Remote - SSH

I installed Remote - SSH, which is a specialized VS Code extension that allows you to establish a secure network connection to a remote computer over the internet. I installed it to link my local VS Code editor directly to my running Amazon EC2 instance, enabling me to use its advanced IDE features to seamlessly browse files, run commands, and edit my web app's files as if they were hosted on my local machine.

### SSH configuration details

Configuration details required to set up a remote connection include a Host nickname, the remote HostName representing the public IP address of your EC2 instance, the login User (such as ec2-user), and the IdentityFile pointing to the absolute path of your private key file. These parameters are saved together inside your local SSH configuration file, allowing VS Code to automatically execute the connection and authenticate your identity without manually typing your SSH command each time.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

### Exploring the project structure

Using VS Code's file explorer, I could see the complete directory structure of our newly generated Java web application hosted on our remote Amazon EC2 instance. At the project root, I observed the pom.xml configuration file, which manages our build settings, alongside the src directory. Navigating deeper into src/main/webapp, I found the index.jsp landing page and WEB-INF directory, illustrating how the Maven archetype had automatically organized our web assets.

Two of the project folders created by Maven are src and webapp, which organize our application's source code and web assets. The src folder acts as the main container for all the source code files defining how our Java web application looks and functions, while the webapp folder sits inside it to hold our public-facing web elements like HTML, CSS, and JSP files that are directly served to a user's browser.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

### What I did in this step

In this step, I will install the Remote - SSH extension in VS Code and use it to establish a remote connection to my running Amazon EC2 instance because we need to utilize VS Code's rich IDE capabilities to browse directories, manage project files, and easily edit our Java web app's index.jsp source code directly on the remote server without relying on terminal-only text editors.

### Updating the web app

The index.jsp file is a server-side document template used in Java web applications to render web pages. While it is structured with standard HTML markup to display static elements, it has the unique ability to execute Java code on the server to generate dynamic content that can adapt to user actions or database updates before being sent to the browser.

I edited index.jsp by opening the file in VS Code, replacing the default placeholder markup with a customized HTML structure that displays a personalized greeting with my name, and saving my changes using the Ctrl + S keyboard shortcut to update the web page files directly on my remote Amazon EC2 instance.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-vscode_7a1de541)

---

## Using nano

### Additional improvements

### Terminal vs IDE

### Verifying my work

---

---

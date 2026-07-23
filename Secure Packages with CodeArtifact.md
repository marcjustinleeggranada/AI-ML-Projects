<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Packages with CodeArtifact

**Project Link:** [View Project](http://nextwork.ai/projects/aws-devops-codeartifact-updated)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Introducing Today's Project!

In this project, I will demonstrate how to set up and configure AWS CodeArtifact as a secure, private repository to manage and cache Java dependencies for a web application. I am doing this project to learn how to secure software packages using IAM policies, establish a reliable repository connection on Amazon EC2, and integrate dependency management into CI/CD pipelines.

### Key tools and concepts

Services I used were AWS CodeArtifact, Amazon EC2, AWS IAM, and GitHub. Key concepts I learnt include setting up a private artifact repository connected to Maven Central as an upstream repository, utilizing IAM policies and roles to securely authorize server access with temporary AWS STS tokens, and configuring Apache Maven via a custom settings.xml file to download and cache Java dependencies.

### Project reflection

This project took me approximately two hours to complete. The most challenging part was troubleshooting the initial connection between my Amazon EC2 instance and the private repository, specifically understanding how Apache Maven authenticates using the settings.xml configuration. It was most rewarding to see the Java dependencies successfully populate the AWS CodeArtifact dashboard during compilation, verifying that our secure software supply chain was fully functional.

This project is part three of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project, Package an App with AWS CodeBuild, tomorrow to learn how to automate our software builds and seamlessly fetch packages from our AWS CodeArtifact repository.

---

## CodeArtifact Repository

AWS CodeArtifact is a fully managed artifact repository service that acts as a secure, private locker for software packages. Engineering teams use artifact repositories because they provide a centralized source of truth for software dependencies, caching approved versions of external libraries to ensure the entire team and the CI/CD pipeline always build applications using consistent, reliable, and secure packages.

A domain is a logical grouping of AWS CodeArtifact repositories that allows an organization to centralize package storage, share dependencies easily, and manage billing and security policies globally. My domain is nextwork, which acts as the administrative boundary for our private Maven repository and houses all our cached Java assets.

An upstream repository is a fallback source that our primary repository automatically queries whenever a requested package is missing. My repository's upstream repository is Maven Central, which allows AWS CodeArtifact to securely fetch, cache, and serve public Java dependencies to our development environment.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codeartifact-updated_n4o5p6q7)

---

## CodeArtifact Security

### Issue

To access AWS CodeArtifact, we need an authorization token that acts as a temporary password to authenticate our development tools. I ran into an error when retrieving this token because my Amazon EC2 instance does not have any default IAM permissions to interact with other AWS services, adhering to the secure principle of least privilege.

### Resolution

To resolve the error with my security token, I created a custom IAM policy with permissions to retrieve authorization tokens and attached it to a new IAM role assigned directly to my Amazon EC2 instance. This resolved the error because it gave our cloud development server the explicit, secure authorization required to request temporary credentials from AWS CodeArtifact, allowing Apache Maven to successfully authenticate and fetch our project dependencies.

Using IAM roles is a security best practice because they rely on temporary, automatically rotated security credentials instead of static, hardcoded keys. This completely eliminates the risk of sensitive AWS credentials being leaked, stolen, or accidentally committed to source control, ensuring our Amazon EC2 instance accesses AWS CodeArtifact securely under the principle of least privilege.

---

## The JSON policy attached to my role

The JSON policy I set up grants permissions to obtain temporary authentication tokens via AWS STS, retrieve repository endpoints, and read software packages from AWS CodeArtifact. These permissions are necessary because they allow our Amazon EC2 instance to securely authenticate, locate, and download cached Java dependencies from our private repository while strictly enforcing the principle of least privilege.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codeartifact-updated_23rp7q8r9)

---

## Maven and CodeArtifact

### To test the connection between Maven and CodeArtifact, I compiled my web app using settings.xml

The settings.xml file configures Apache Maven to redirect its dependency requests from public registries to our private AWS CodeArtifact repository. It specifies the unique repository endpoints, sets up active execution profiles, and passes the required authentication credentials using the CODEARTIFACT_AUTH_TOKEN environment variable, enabling secure and automated retrieval of Java packages for our application builds.

Compiling is the process of translating human-readable source code written in Java into machine-readable bytecode that the execution environment understands. During this compilation phase, Apache Maven also reads our project's configuration, automatically resolves and retrieves all required software dependencies, and prepares the runnable application binaries that can be safely executed on our Amazon EC2 instance.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codeartifact-updated_c17eace8)

---

## Verify Connection

After compiling, I checked my private AWS CodeArtifact repository, specifically the Packages tab in the AWS Console. I noticed that the repository was newly populated with multiple Maven packages, confirming that CodeArtifact had successfully fetched the required Java dependencies from our upstream repository (Maven Central) and cached them securely in our private domain.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Uploading My Own Packages

---

---

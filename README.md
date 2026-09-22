<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](https://nextwork.ai/projects/b71d29bd-8a1b-5fe0-9572-1c575423d558)

**Author:** Abdul Hussein  
**Email:** abdulhussein@hotmail.se

---

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_7a1de541)

## Introducing Today's Project!

In this project, I demonstrated how to launch an EC2 instance on AWS, connect to it from VS Code using Remote - SSH and a key pair, and install Java and Maven to generate a Java web app. I will also show how I edited the app's index.jsp file to customize the page and see it running in the cloud.



I did this project because I want to build hands-on DevOps skills, and it's the first step in a CI/CD pipeline series.

### Key tools and concepts

Services I used were Amazon EC2, for a cloud server to develop on, and VS Code with Remote - SSH to connect to it. Key concepts I learnt include key pairs and SSH for secure access, using an SSH config file to save connection details, and installing Java and Maven to generate a web app project with its pom.xml and index.jsp. This is the foundation for building a CI/CD pipeline.

### Project reflection

This project took me approximately 1 hour since it was the first time for me.

One thing I didn't expect was how much Maven generates from a single command.

## Launching an EC2 instance

### What I did in this step



I started this project by launching an EC2 instance because my web app needs somewhere to actually run. EC2 gives me a virtual server in the cloud that I can control: I choose the operating system, connect to it remotely, and install the tools and software my app needs.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_7852fbf3)

### I also enabled SSH

I enabled SSH so I can securely connect to my EC2 instance from my own computer and run commands on it. SSH encrypts the connection and checks that I have the private key matching the public key on the server, so only authorized users can get in. I'll need this connection later in the project to install software and set up my web app on the server.

### Key pairs

A key pair in EC2 is like the keys to your virtual computer. Just like you need a key to unlock and start your car, a key pair lets you securely access your EC2 instance.

It's made of two halves: a public key that AWS keeps, and a private key that you download.

When you use the private key, it verifies that you're the one allowed to access that specific virtual machine, keeping everything secure and just for you.

### Downloaded key pair file

Once I set up my key pair, AWS automatically downloaded the key pair as a .pem file. 

## Set up VS Code

### What I did in this step

In this step, I set up my development environment so I can connect to my EC2 instance. I downloaded and installed VS Code, which is where I'll write and manage code, and opened a terminal inside it so I can run commands. I also changed the permissions of my .pem key file (using chmod 400) so that only I can read it.

### What is VS Code?

Visual Studio Code (VS Code) is one of the most popular tools for creating and managing coding projects. You'll often hear people call VS Code an IDE (Integrated Development Environment), which means software that help you write and edit code.

I used VS Code as my development environment for the whole project.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_53d05e68)

## My first terminal commands

A terminal is where you send instructions to your computer using text instead of clicks. For example, instead of right-clicking on your desktop to create a new folder, you can type a simple text command in your terminal instead. It's like sending text messages to your computer's operating system to tell it what to do.

The first command I ran for this project was cd %USERPROFILE%\Desktop\DevOps

### Updating file permissions

I also updated my private key's permissions by running following commands in the terminal:

icacls "nextwork-keypair.pem" /reset
icacls "nextwork-keypair.pem" /grant:r "Enter your username:R"
icacls "nextwork-keypair.pem" /inheritance:r

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_9328ada1)

## SSH connection to EC2 instance

### What I did in this step

In this step, I connected to my EC2 instance from the VS Code terminal using SSH and my .pem key file, because I need a secure way to access the server and run commands on it.

### Connecting to EC2

To connect to my EC2 instance, I ran the command ssh -i [[path to the -pem file]] ec2-user@"PUBLIC IPV4 DNS of the ec2 instance"

### This command required an IPv4 address

A Public IPv4 DNS (which stands for Domain Name System) is the public address for your EC2 server that the internet uses to find and connect to it. The local computer you're using to do this project will find and connect to your EC2 instance through this IPv4 DNS.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_e3069dca)

## Maven & Java

### What I did in this step

In this step, I installed Apache Maven and Amazon Corretto 8 on my EC2 instance, then verify both installations, because my web app needs them to be built and run. Maven is a build tool that compiles the code, manages dependencies, and packages the app, which is what the CI/CD pipeline will later automate. Corretto 8 is Amazon's version of Java, which Maven and the app depend on. Verifying the installations confirms the server is ready before I create the web app.

### Why I'm using Maven

Apache Maven is a powerful tool that automates the building of software.

Maven is required in this project because it's a build tool that automates the work of turning my Java web app's source code into something that can run on a server. It compiles the code, downloads the libraries the app depends on, and packages everything into a deployable file (a WAR). Maven also generates the standard project structure, so I don't have to set up folders and configuration by hand.

### Why I'm using Java

Java is a popular programming language used to build different types of applications, from mobile apps to large enterprise systems.

Java is required in this project because my web app is a Java application, and Maven is also built on Java, so neither can run without it.

## Create the Application

### What I did in this step

In this step, I ran Maven commands in my terminal to generate a Java web app, because I needed a working project to build, test, and later deploy through the CI/CD pipeline.

### Creating the Java web app

I generated a Java web app using the command:

mvn archetype:generate \
   -DgroupId=com.nextwork.app \
   -DartifactId=nextwork-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false

This command tells Maven to create a new project from a template, called an archetype. -DgroupId=com.nextwork.app set the package name that identifies my project. -DartifactId=nextwork-web-project set the project's name, which is also the name of the folder Maven created. -DarchetypeArtifactId=maven-archetype-webapp chose the template for a basic Java web app. -DinteractiveMode=false made Maven use my values instead of asking me questions.

### Installing Remote - SSH

I installed Remote - SSH so I could edit and run code directly on a remote machine from my local editor, instead of copying files back and forth or working in a bare terminal.

### SSH configuration details

Configuration details required to set up a remote connection include a Host alias (a short nickname for the server), the HostName (the server's IP address or domain), and the User I log in as. It also specifies the Port if it isn't the default 22, and an IdentityFile pointing to my private SSH key so I can authenticate without typing a password.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_2939cf01)

## Create the Application

### Exploring the project structure

Using VS Code's file explorer, I could see all the folders and files that we Maven created when we ran the build command earlier.

The src (source) folder holds all the source code files that define how your web app looks and works.

While webapp folder holds web app's files e.g. HTML, CSS, JavaScript, and JSP files,

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_45f91fd7)

## Using Remote - SSH

### What I did in this step

In this step, I installed an extension in VS Code (Remote - SSH), used it to connect VS Code to my EC2 instance, and then explored and edited my Java web app's files, because I wanted a much easier way to manage my code on the server than typing terminal commands.

### Updating the web app

index.jsp is a file used in Java web apps. It's similar to an HTML file because it contains markup to display web pages.

However, index.jsp can also include Java code, which lets it generate dynamic content.

I edited index.jsp by changing the content via VS Code with my own text.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/b71d29bd-8a1b-5fe0-9572-1c575423d558_7a1de541)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/b71d29bd-8a1b-5fe0-9572-1c575423d558)*

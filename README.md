# CI-CD-with-Jenkins-Ansible-Docker-on-AWS

<h2>Introduction</h2>

**Tools**</br>

1.**Git** - Local version control system</br>
2.**GitHub** - Distributed version control system</br>
3.**Jenkins** - Continuous integration tool</br>
4.**Maven** - Build tool</br>
5.**Ansible** - Configuration management and deployment tool</br>
6.**Docker** - Containerisation</br>
Setup all these environments on AWS</br>

<h4>Resources to setup Devops CI/CD pipeline</h4></br>

- AWS free tier account</br>
- GitHub account</br>
- MobaXterm- For Windows user.For MAC and Linux user- Terminal will work.</br>
- Git Installed.</br>

<h2>Devops Workflow</h2>

![proj_2](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/b249aa7c-0e64-47f6-ba71-924129aab92a)

<h2>Steps to be followed:</h2>

<h3>Create AWS instances</h3>

First we need to launch Four  instances on AWS for one for Git,one for Jenkins, one for Ansible and one for Docker separately.

![Screenshot (892)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/8a61e6a6-87a7-4996-b9a0-195d23c28b1b)

![Screenshot (887)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/edd939fa-cbb2-4073-b4c0-7b7d0af2cf8e)

![Screenshot (885)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/cc941220-83c7-4d9e-9fe4-ca9f253b520e)

![Screenshot (891)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/113cfb09-afdd-43b4-aa16-48f89f234e86)

![Screenshot (898)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/873bd5d7-7d33-4eb5-a03c-d05921a87c47)


Git-server
Prerequisites:
1.Git

Jenkins-server: 

Prerequisites:

 1.Install Jenkins,
2.Java, 
3 Maven
4.Git
configure it in jenkins global tool configuration


Docker-server:
Prerequisites:
1.Install Docker 

Add User in Docker Server
Set a password for the user

Adding the user to 'docker' group allows the user to run any docker command without using 'sudo'.


Ansible-server:

Prerequisites:

1.Install Ansible 
2. Install Docker.

Add User and  Set a password for the user - The user you create here will be used by Jenkins to SSH into the Ansible server for executing commands related to container creation.

Root user: Enable Password-Based Authentication

vi /etc/ssh/sshd_config
save and close the file.
service sshd reload

Add Ansible Server in Jenkins

Create Dockerfile



After installing Docker, add the 'ansadmin' user to the 'docker' group.

By adding the user to the 'docker' group, you allow them to execute Docker commands without requiring root privileges.

This means you won't need to use 'sudo' each time with Docker commands.

you are logged in as the root user.we need to add the target servers to the /etc/ansible/hosts file.

then switch to 'ansadmin' user:

log in to Docker Hub:   using command -->docker login

By executing the above command, you will successfully log in to your Docker Hub account. Now your Ansible server is configured to access Docker Hub for uploading Docker images.

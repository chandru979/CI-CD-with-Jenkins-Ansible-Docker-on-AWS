# CI-CD-with-Jenkins-Ansible-Docker-on-AWS

<h2>Introduction</h2>

**Tools**</br>

1. **Git** - Local version control system</br>
2. **GitHub** - Distributed version control system</br>
3. **Jenkins** - Continuous integration tool</br>
4. **Maven** - Build tool</br>
5. **Ansible** - Configuration management and deployment tool</br>
6. **Docker** - Containerisation</br>
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

First need to launch Four instances on AWS [Ubuntu OS for Git, Amazon Linux OS for Jenkins, Amazon Linux OS for Ansible and Amazon Linux OS for Docker] separately.

![Screenshot (892)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/8a61e6a6-87a7-4996-b9a0-195d23c28b1b)

![Screenshot (887)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/edd939fa-cbb2-4073-b4c0-7b7d0af2cf8e)

![Screenshot (885)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/cc941220-83c7-4d9e-9fe4-ca9f253b520e)

create Security group for all instance and open port of 8080 for jenkins-server, 8082 for docker-server(tomcat)
![Screenshot (891)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/113cfb09-afdd-43b4-aa16-48f89f234e86)

![Screenshot (898)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/873bd5d7-7d33-4eb5-a03c-d05921a87c47)

Now that we have created instances for running Git, Jenkins, Ansible, and Docker, we will proceed to install and configure the applications on these instances

<h3>Connect Instances using SSH client in Mobaxterm</h3>

![Screenshot (899)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/dd393679-07db-4ba5-96cd-3f680e8bbfc1)

GO to **Click -> SSH** and then **Remote host ->** Paste your ssh, **Click-> Advanced SSH settings -> Use private key ->** paste PEM key for openSSH.  
![Screenshot (919)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/df53d44c-50a3-4fa6-9461-fb12d9f6b5bc)


<h3>Git-server:</h3>
Prerequisite:</br>

1. Install Git

<h3>Jenkins-server:</h3> 
Prerequisites:</br>

1. Install Jenkins
2. Install Java
3. Install Maven
4. Install Git
5. configure it in jenkins global tool configuration
6. Install required Plugins in jenkins

Open Jekins with **Public IP** address of jenkins-server added with (**:8080**) -> (Example: 172.25.85.01:8080) </br>
- Unlock Jenkins:</br>
To get the password, run this command in your terminal: **sudo cat /var/lib/jenkins/secrets/initialAdminPassword**. After entering the password click on continue.

![Screenshot (851)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/90ecda53-88f8-456c-8bf7-682c27145b4b)

![Screenshot (853)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/5fbdf89d-6bff-4f91-87ad-336e0dbc8bc3)

- Create First Admin user:</br>
![Screenshot (854)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/892f5d81-5686-4390-9e19-85ec4c6a5d60)

After enter username and password **Click -> Sign in**:
![Screenshot (927)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/1ab1b0c0-f64a-4fef-857e-48057a0af2ac)

Afer Instllating of JDK, Maven add directories to Jenkins. </br> 
Go to **Manage jenkins -> Tools** (Add JDK and Add Maven Path directory)</br>
![Screenshot (908)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/14f13c5c-9da5-4ef8-8f6e-7dc9e2131a26)

![Screenshot (909)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/6136d4df-4ea6-410f-b4f5-3631218d1f5f)

![Screenshot (910)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/f5975d63-2708-48dc-a65e-1eadf9b6ae40)

Next install plugins, </br>
Go to **Manage Jenkins -> Plugins -> Select Available Plugins ->** search (Maven Integration, GitHub, Publish over SSH) -> Click on **'Install without restart'**

![Screenshot (912)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/ef05ab86-6b18-4f75-9297-9a5d7b1ccc76)

![Screenshot (914)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/fa367e7e-391d-421b-beba-d42bce0e2700)


<h3>Docker-server:</h3>
Prerequisite:</br>

1. Install Docker 

Add User in Docker Server
Set a password for the user

Adding the user to 'docker' group allows the user to run any docker command without using 'sudo'.


<h3>Ansible-server:</h3>
Prerequisites:</br>
The commands are in the above file called (Ansible-server.rtf)</br> 
1. Install Ansible 
2. Install Docker.

Add User(ansadmin) and Set a password for the user - 

To grant root privileges to the **'ansadmin'** user, execute the following command: **sudo usermod -aG sudo ansadmin**</br>
command: **visudo**


![Screenshot (861)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/31060902-7bdb-42e9-829d-f561cfc484ba)

- From Root user: Enable Password-Based Authentication

command: **vi /etc/ssh/sshd_config** </br>
**Click -> i** to modify the file and search for **passwordAuthentication - > yes**
![Screenshot (859)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/343a190a-336f-4451-bf0b-82b510a80ec3)

save and close the file.
command:**service sshd reload**

Add Ansible Server in Jenkins

Create Dockerfile



After installing Docker, add the 'ansadmin' user to the 'docker' group.

By adding the user to the 'docker' group, you allow them to execute Docker commands without requiring root privileges.

This means you won't need to use 'sudo' each time with Docker commands.

you are logged in as the root user.we need to add the target servers to the /etc/ansible/hosts file.

then switch to 'ansadmin' user:

log in to Docker Hub:   using command -->docker login

By executing the above command, you will successfully log in to your Docker Hub account. Now your Ansible server is configured to access Docker Hub for uploading Docker images.

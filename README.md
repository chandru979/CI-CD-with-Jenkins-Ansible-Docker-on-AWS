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

- Need to **connect your remote repo** of project folder in git-server.</br>
- Using **PollSCM** in jenkins server that is used for **Continuous Integration** using git-server. If any chances made in the project file that will automatically build the job in jenkins server is called comtinuous integration.

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

- After Installing Docker, need to start the docker service: 
command: **service docker start**

Add User(ansadmin) and Set a password for the user </br>

Once we have created the user, it’s time to grant sudo access to it.</br>
command: **visudo** </br>
Go to the  file and paste the below-mentioned line as it is:</br>
**ansadmin ALL=(ALL)       NOPASSWD: ALL**

![Screenshot (861)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/31060902-7bdb-42e9-829d-f561cfc484ba)

- From Root user: Enable Password-Based Authentication

command: **vi /etc/ssh/sshd_config** </br>
**Click -> i** to modify the file and search for **passwordAuthentication - > yes**
![Screenshot (859)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/343a190a-336f-4451-bf0b-82b510a80ec3)

save and close the file.</br>
command:**service sshd reload**

Adding the user to 'docker' group allows the user to run any docker command without using 'sudo'. </br>

By adding the user to the 'docker' group, you allow them to execute Docker commands without requiring root privileges.</br>

This means you won't need to use 'sudo' each time with Docker commands.</br>


<h3>Ansible-server:</h3>
Prerequisites:</br>
The commands are in the above file called (Ansible-server.rtf)</br> 
1. Install Ansible </br>
2. Install Docker.

Add User(ansadmin) and Set a password for the user. </br> 

Once we have created the user, it’s time to grant sudo access to it.</br>
command: **visudo** </br>
Go to the  file and paste the below-mentioned line as it is:</br>
**ansadmin ALL=(ALL)       NOPASSWD: ALL**

![Screenshot (861)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/31060902-7bdb-42e9-829d-f561cfc484ba)

- From Root user: Enable Password-Based Authentication</br>

command: **vi /etc/ssh/sshd_config** </br>
**Click -> i** to modify the file and search for **passwordAuthentication - > yes**
![Screenshot (859)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/343a190a-336f-4451-bf0b-82b510a80ec3)

save and close the file.
command:**service sshd reload**

- Now, log in as an ansadmin user:</br>
**su - ansadmin**
Use ssh-keygen command to generate key:</br>
**ssh-keygen**
  
- Setting Ansible Inventory:</br>
The default location for the inventory resides in /etc/ansible/hosts.</br>
Go inside file -> **vi /etc/ansible/hosts**.</br>
For **dockerhost -> 'private_ip_of_docker-server',   ansible -> 'private_ip_of_ansible-server'** </br>

![Screenshot (923)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/09f3b976-3ca6-444f-9e99-df8f5d9811ed)

- ssh-copy-id is a useful tool for SSH connections to a remote host without using a password.</br>

command: **ssh-copy-id private_ip_docker-server**</br>
command: **ssh-copy-id private_ip_ansible-server**

 - Test our Ansible Inventory: </br>
   using **ansible all -m ping** </br>

![2](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/1ea2ac77-c8f3-4999-8667-843e0f3b9830)


Integrating Ansible with Jenkins:</br>

**Configure System ->** find **Publish over SSH** **-> SSH Servers ->**click on the **Add button**. </br>
Enter **Name -> ansible**, **Hostname ->** 'pritvate_ip_ansible-server', **username** -> Enter created username of ansible-server **'ansadmin'**, **Click -> Advanced ->checkin password Authentication -> password ->** Enter created password of ansible-server **-> Apply & Save**.

![Screenshot (934)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/4e1b883e-a83b-48c5-9e23-316746196f05)

![Screenshot (935)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/8aef55f3-a65d-49b8-ab0d-d78c0a3673c5)

![Screenshot (936)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/422e0acf-1095-4f92-9eae-b108a1f88882)


- Goal is to send the war file to the specified directory to your Ansible server:</br>
  Create directory</br>
**sudo su
mkdir /opt/docker
chown ansadmin:ansadmin /opt/docker -R**

/opt/docker -> will be used as our workspace, where Jenkins will upload the artifacts to Ansible Server.</br>

<h4**>Creating Dockerfile and Ansible Playbook:** (Files are in the above) </br></h4>

To create a Docker Image with the webapp.war file, first, we will create a DockerFile.</br>

- command to create dockerfile: **vi dockerfile** </br>
With the help of this Dockerfile, we will create a Docker container</br>

We are creating a Ansible Playbook, which does two tasks for us:</br>

- command to create yaml file: **vi filename.yml or vi filename.yaml** </br>

![1](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/59e6d02d-0068-4587-98d2-1674f0f04c21)

Pull Tomcat’s latest version and build an image using webapp.war file.</br>
Run the built image on the desired host.</br>

**Pushing Docker Image to Docker Hub Using Ansible:** </br>
- create one new Ansible Playbook which will build and push the Docker image to your Docker Hub account.</br>
  **vi regapp.yaml**

command: **docker login** for connect DockerHub account.</br>

Go to your Docker Hub account and see if the image was pushed successfully</br>

![Screenshot (948)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/d382c8b3-93c6-4300-8b7c-ce82c3610cb6)

- create another new Ansible Playbook, we are going to pull the Docker image from Docker Hub Account and create a container out of it.</br>
  **vi deploy_regapp.yaml**


<h3> Jenkins Jobs to Deploy Docker Container Using Ansible </h3></br>

**Click -> New Item** to create a job</bd>
**Enter -> item name** </br>
**click -> Maven project** </br>
![Screenshot (937)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/5920cf9d-ae6a-4e48-a6e4-898c0f9e7508)

- In section **Source code Management -> Git ->** paste your github link
![Screenshot (939)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/8894feec-eb4a-4a8e-b02d-6c2a9dadbb81)

- In section **Build Triggers -> select -> poll SCM -> * * * * * ,**
![Screenshot (941)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/ae53805e-b707-4366-8f71-43142e9f82a6)
- In section **Build -> Goal and options -> clean install package**
![Screenshot (942)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/b898f40d-5560-4146-a5f3-654b06739d80)
- In section **Add post Build action -> send build artifacts over SSH**
![Screenshot (943)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/58bf28db-3fbc-41bf-a2d1-de20fa904d59)
- Add ansible server you already integrate with jenkins configure: </br>
![Screenshot (944)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/b539077d-d9e5-4ae5-8feb-346380be6cad)
In **Transfer set section -> Add -> Source files, Remove prefix, Remote directory**:</br>
- Exec command - used for automated the process of Push and pull image, build image, run container(tomcat):

![Screenshot (945)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/02df3b45-8ac7-48da-b75e-52bc3b2145f5)

- **Click -> Build Now** or **Play Button** on right side of the job to buils a job 
![Screenshot (954)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/63aac8ae-a38f-4a70-b8f3-03366dd81a50)

- Go to the console output to see final result : **Success or not**
![Screenshot (949)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/12a076d4-75ac-45b5-91a4-93f5fa07e483)

- To access the web application using Docker **public_ip_address** with (enabled port for docker and tomcat server)</br>

![Screenshot (951)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/29c277ee-69d4-447e-b47b-0129623d709d)

![Screenshot (952)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/3cd093fc-78e6-4a47-83e6-2f1a68f8a201)

![Screenshot (953)](https://github.com/chandru979/CI-CD-with-Jenkins-Ansible-Docker-on-AWS/assets/79323743/a30498d2-861b-426f-ac11-82e327aacf9d)



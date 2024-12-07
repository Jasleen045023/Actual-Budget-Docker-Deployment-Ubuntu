# OS Installation with Docker (Ubuntu)




<h1>About the Project</h1>

The project focused on installing and running the "Actual Budget" application using Docker technology. The aim was to streamline the deployment process by leveraging Docker's containerization capabilities, ensuring the application operates consistently across different environments. To accomplish this, I utilized Ubuntu operating system within a VirtualBox environment to execute Docker commands.

The key tasks in this project included pulling the necessary Docker images, creating containers, and configuring them to run the application seamlessly. This approach provided a lightweight and efficient solution for managing dependencies, reducing setup time, and ensuring scalability. By using Docker, the project demonstrated how containerization simplifies application deployment, making it reliable and portable across platforms.




<h1>Learning Objectives</h1>
<ol>
<li>Docker Commands: Learned to use Docker commands like docker pull, docker run, and docker ps to containerize and deploy the "Actual Budget" application.</li>
<li>Container Management: Gained proficiency in managing containers by configuring environment variables, monitoring logs, and troubleshooting errors using docker logs and docker exec.</li>
<li>Ubuntu CLI Operations: Acquired hands-on experience in executing and managing Docker-related tasks using the Ubuntu command line within a VirtualBox setup.</li>
<li>Efficient Dependency Management: Implemented containerized solutions to streamline dependencies and eliminate environment-specific issues during application installation and execution.</li>
<li>Application Deployment Workflow: Developed and tested a complete deployment workflow for the "Actual Budget" app, ensuring consistent performance across different environments.</li>
</ol>




<h1>About the Application - Actual Budget</h1>

The "Actual Budget" application is a robust personal finance tool designed to help users take control of their finances with precision and ease. Unlike many budgeting tools, it’s privacy-focused and works entirely offline, so your financial data stays safe and secure on your own device. The application offers features such as real-time updates, customizable budgeting, and detailed reporting. It empowers users to track their spending, manage their income, and plan for future expenses effectively. The powerful reporting tools provide clear insights into financial habits, enabling informed decisions. 




<h1>Pre-Requisites</h1>
<ol>
<li>Operating System: Ubuntu (or any compatible Linux distribution) installed within a VirtualBox environment.</li>
<li>Required Software and Tools: Docker (including Docker CE, Docker Compose, and containerd) and Git for version control (installed using sudo apt) along with cURL for downloading Docker GPG keys.</li>
<li>System Requirements: Adequate disk space to install Docker and create working directories for the "Actual Budget" application and a sufficient memory and CPU resources to run Docker containers smoothly.</li>
<li>File System Configuration: Pre-created working directories (~/docker/actualbudget/data) for storing application data and a valid config.json file, even if it’s initially empty. Correct ownership and permissions set for the directories (chown and chmod commands).</li>
<li>Docker Image and Port Setup: The Docker image for the "Actual Budget" application (actualbudget/actual-server) must be available for download. Port 5006 on the host system should be free and open for application access.</li>
</ol>




<h1>Commands Executed</h1>

### **install prerequisites**
```
sudo apt install apt-transport-https ca-certificates git curl software-properties-common gnupg-agent -y
```

### **add docker gpg key**
```
curl -fsSL https://download.docker.com/linux/$(awk -F'=' '/^ID=/{ print $NF }' /etc/os-release)/gpg | sudo apt-key add -
```

### **add docker software repository**
```
sudo add-apt-repository "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/$(awk -F'=' '/^ID=/{ print $NF }' /etc/os-release) $(lsb_release -cs) stable"
```

### **install docker**
```
sudo apt install docker-ce docker-compose containerd.io -y
```

### **enable and start docker service**
```
sudo systemctl enable docker && sudo systemctl start docker
```

### **add the current user to the docker group**
```
sudo usermod -aG docker $USER
```

### **reauthenticate for the new group membership to take effect**
```
su - $USER
```

### **create working directories**
```
mkdir ~/docker/actualbudget/data -p
```

### **create config.json**
```
touch ~/docker/actualbudget/config.json
```

### **write empty config file**
```
echo "{}" > ~/docker/actualbudget/config.json
```
```
cat ~/docker/actualbudget/config.json
```

### **set owner of working directories**
```
sudo chown "$USER":"$USER" ~/docker -R
```

### **allow the container to write to working directories**
```
sudo chmod a+rwx -R ~/docker/actualbudget
```

### **run actual budget container**
```
docker run -d --name actualbudget -p 5006:5006 -v ~/docker/actualbudget/config.json:/app/config.json -v ~/docker/actualbudget/data:/data --restart=unless-stopped actualbudget/actual-server
```

```
docker ps
```




<h1>Steps to Access the Application - Actual Budget</h1>
<ol>
<li>Open the browser and navigate to localhost:5006.</li>
<li>Click on the Advanced Options link.</li>
<li>Check the "I understand the risks" box > Click Open Actual.</li>
<li>Enter and confirm the password.</li>
<li>Complete the installation and log in then, navigate to "Reports".</li>
</ol>




<h1>Video</h1>

https://github.com/user-attachments/assets/d755fb48-7443-47be-8247-5b8bb0e4673c




<h1>Acknowledgements</h1>

Special thanks to:
<ol>
<li>Prof. Ashok Harnal (Faculty - Information Systems, FORE School of Management): For sharing valuable insights on Docker-based deployment techniques.</li>
<li> [i12bretro](https://github.com/i12bretro): For providing a video tutorial that guided the successful Docker deployment on Ubuntu.</li>
</ol>

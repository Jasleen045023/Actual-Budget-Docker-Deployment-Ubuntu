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




https://github.com/user-attachments/assets/5a8083f3-a4b3-4957-b925-6bd55a1584d9




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

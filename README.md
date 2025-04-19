# Managing-Users-and-Groups-on-an-Amazon-Linux-EC2-Instance


![EC2Instance (1)](https://github.com/user-attachments/assets/a0a72f38-3477-4027-9dc0-c17f0692fb61)

Setting up a solid cloud environment starts with choosing the right compute resources. In this project, I launched and set up my first Amazon EC2 instance. I made decisions that balanced performance, cost, and security, like picking the right instance type, setting up the network and storage, and applying security rules. 
Each step followed best practices to make sure everything worked smoothly.

This documentation walks through the entire process and explains why I made certain choices, and how they affected the setup overall.

---

## Step 1: Select a Region
After logging into the AWS Management Console, I went to the EC2 service and chose a region. I picked one based on things like speed (latency) and backup options (redundancy) to make sure my instance would run smoothly and perform well.

![Screenshot (108)](https://github.com/user-attachments/assets/224e62b0-91db-4c2a-a3f5-a3aecb279641)

## Step 2 & 3: Naming the EC2 Instance & Choosing an Amazon Machine Image(AMI)
I gave my instance a simple name,"MyFirstInstance" so I could easily recognize it later. For the next step, I chose an Amazon Machine Image (AMI), which comes with the operating system and basic software already set up. AWS offers ready-made AMIs, but you can also create your own or use ones from the AWS Marketplace.

![Screenshot (109)](https://github.com/user-attachments/assets/63fa730d-60a4-4233-82e3-a0b6e10d0809)

## Step 4: Choosing the Right EC2 Instance Type
AWS has many instance types, so it’s important to choose one that matches your app’s needs for CPU, memory, storage, and network speed. If you choose too little, it might run slow. If you choose too much, you’ll waste money. For this project, I picked a t2.micro instance (1 vCPUs, 1 GiB RAM) because it’s free tier eligible and a good balance between cost and performance.

![Screenshot (111)](https://github.com/user-attachments/assets/495c2c40-642a-45a5-ba75-a5bfe3f52c71)

## Step 5: Configuring Secure Access with a Key Pair
To keep my instance secure, I created a key pair. AWS uses this to control access using public and private keys. I downloaded the private key to use later to connect safely to the instance. Setting this up during launch makes sure only I could access the server.

![Screenshot (112)](https://github.com/user-attachments/assets/28b4ebf3-25ba-44bc-b894-64e132dd8c50)

## Step 6: Setting Up Networking and Security
The network settings decide how my instance can be reached and how secure it would be. I placed it inside a default VPC and made a security group called "my-first-instance-sg" to control who can connect. This security group acts like a firewall, managing traffic in and out.

![Screenshot (114)](https://github.com/user-attachments/assets/31d14116-17a0-4447-897d-d9d849c5bd65)

## Step 7: Adding Storage
For storage, I used Amazon EBS and kept the default 8 GiB root volume. This gave enough space for the web server while keeping costs low. I can always add more storage later if needed.

![Screenshot (115)](https://github.com/user-attachments/assets/925bdf0e-a885-49ab-a651-03d11179667b)

## Step 8: Configuring Advanced Settings
To automate the setup, I used user data scripts that ran when the instance launched. The script:
-Installed Apache (httpd)
-Started and enabled the web server
-Deployed a simple HTML page to confirm the server was working
This made the setup automatic and saved time by removing manual steps.

![Screenshot (116)](https://github.com/user-attachments/assets/7885cb4b-f4e9-4422-bf4e-bd55899e1c17)

## Step 9: Launching the Instance
After completing the setup, I launched the instance, and it quickly transitioned from "Pending" to "Running," confirming everything was configured correctly. A public DNS name was assigned, allowing internet access. However, I didn't enable termination protection, which is an option that can be used to prevent accidental termination of the instance for added security.

![Screenshot (117)](https://github.com/user-attachments/assets/90be298c-1241-4107-8334-d746df97d4c3)

## Step 10: Monitoring the Instance
I monitored the instance to ensure it was running smoothly. In the EC2 Status Checks tab, I verified that both system and instance checks passed. I also used Amazon CloudWatch to track real-time metrics, giving me insights into resource usage.

![Screenshot (118)](https://github.com/user-attachments/assets/e6cc26a8-fa87-4e97-8b7e-f0c1e6678d19)

## Step 11: Enabling Web Access
At first, HTTP requests were blocked because of security group settings. To fix this, I updated the security group to allow inbound traffic on port 80, making the web server accessible through its public IP. This step emphasized the importance of least privilege access, giving only the permissions needed.

![Screenshot (120)](https://github.com/user-attachments/assets/a58488ed-7fe6-46df-a909-e2af74fb970a)

## Step 13: Connecting via ssh - Instance connect
The SSH port (22) was already open by default in the security group, so I was able to connect to the instance using EC2 Instance Connect directly from the AWS Console. This made it quick and easy to access the server without needing to use a key file. The key file can also be used by connecting via the session manager or ssh client.

![Screenshot (122)](https://github.com/user-attachments/assets/1cf46d37-92c4-45e9-97b0-ccd2bf6f0c0e)

## Step 13: Testing Termination Protection
After I was done with the project, I terminated the EC2 instance from the AWS Console to avoid any extra charges. When an instance is terminated, the attached EBS volume (root storage) is also deleted automatically, unless set otherwise. This helps keep the environment clean and cost-effective.

![Screenshot (124)](https://github.com/user-attachments/assets/3ba61be3-c2ab-4078-b432-72f4176b6a4e)
![Screenshot (126)](https://github.com/user-attachments/assets/ef143320-6b50-43aa-9d9e-0b6a65b57101)

---

### Reflection
This project was a great hands-on experience and gives a great hands-on experience to work with Amazon EC2. It teaches how to launch, configure, and connect to an instance, as well as security, and automation through user data scripts. Each step helps to better understand how cloud resources can work together.

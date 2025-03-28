### **Task 1: Launch a Windows EC2 Instance and Connect Using Key Pair
**
---

###**Task 2: Change the Password of Administrator**

1. Change Password of Administrator:  
2. Test Login with New Password:  
   - Disconnect the RDP session.  
   - Reconnect using the new password instead of retrieving it from the key pair.  
   - Verify both methods:  Ans..???
     - Login using the key-pair-generated password.  
     - Login using the custom password.

---

###**Task 3: Create a New User with Administrator and Remote Desktop Permissions**

1. Create a New User:  
   - Open Computer Management → Local Users and Groups → Users.  
   - Right-click and select New User.  
   - Fill in the details (e.g., `Username: JohnDoe`, Password: `UserPassword123`).  
   - Uncheck User must change password at next logon.

2. Assign Local Administrator Rights:  
   - Go to Local Users and Groups → Groups.  
   - Double-click Administrators → Add the new user (`JohnDoe`) to the group.

3. Grant Remote Desktop Permissions:  
   - Go to System Properties → Remote Settings.  
   - Under Remote Desktop, click Select Users → Add the new user (`JohnDoe`).

4. Test Login with New User:  
   - Open a new RDP session.  
   - Login with the new user credentials (`JohnDoe` and `UserPassword123`).  
   - Verify simultaneous access with both the Administrator and the new user.

---

###**Task 4: Install IIS and Deliver a Web Page (Optional)**

1. Install IIS:  
   - Open Server Manager → Manage → Add Roles and Features.  
   - Select Role-based or feature-based installation.  
   - Choose the current server.  
   - Enable Web Server (IIS) and proceed with the default features.  
   - Complete the installation.

2. Deploy a Web Page:  
   - Open File Explorer → Navigate to `C:\inetpub\wwwroot`.  
   - Replace or edit the `index.html` file with your custom webpage content:  
   
     ```html
     <!DOCTYPE html>
     <html>
     <head>
         <title>IIS-Task </title>
     </head>
     <body>
         <h1>Welcome to "AWS with Avinash Reddy" Trainings. Mater your cloud skills.!</h1>
         <p>Delivered Webpage via AWS EC2 Instance</p>
     </body>
     </html>
     ```

3. Open Security Group for HTTP:  
   - Add a rule in the instance’s security group to allow HTTP (port 80) traffic from Anywhere.

4. Access the Web Page:  
   - Open a browser and navigate to the Public IP of the EC2 instance (e.g., `http://<Public-IP>`).  
   - The custom webpage should be displayed.


---

### **Task 1: S3 Bucket Creation and Replication**
1. **Objective:**  
   - Create an S3 bucket in the **Mumbai (ap-south-1)** region. Enable versioning on the bucket.  
   - Create another S3 bucket in the same region (**Mumbai**) and configure **Same-Region Replication (SRR)** between these buckets.  

2. **Steps to Perform:**  
   - Create the source bucket and enable versioning.  
   - Create the destination bucket in the same region.  
   - Configure the replication rule to replicate objects from the source bucket to the destination bucket.  

3. **Validation:**  
   - Upload objects to the source bucket and verify they are replicated to the destination bucket.

---

### **Task 2: Lifecycle Management Rules**
1. **Objective:**  
   - Create lifecycle management rules for an S3 bucket to optimize storage.  

2. **Requirements:**  
   - For **current version objects**, transition them from **S3 Standard** to **Delete** after **2 days**.  
   - For **previous version objects**, transition them to **Delete** after **1 day**.

3. **Steps to Perform:**  
   - Create an S3 bucket and enable versioning.  
   - Add lifecycle rules for current and previous version objects as specified.  

4. **Validation:**  
   - Verify that objects transition and are deleted as per the configured lifecycle rules.

---

### **Task 3: IAM Policy for Region-Restricted Bucket Creation**
1. **Objective:**  
   - Create an IAM policy that allows all S3 actions but restricts the user to creating buckets **only in the Mumbai (ap-south-1) region**.  

2. **Steps to Perform:**  
   - Create a custom IAM policy by copying permissions from **S3FullAccess** and restricting bucket creation to the **Mumbai** region.  
   - Attach the policy to a newly created IAM user.  
   - Log in as the IAM user and attempt the following:  
     - Create a bucket in **Mumbai** – this should be allowed.  
     - Attempt to create a bucket in any other region – this should be denied.  

3. **Validation:**  
   - Ensure the policy behavior is as expected:  
     - Bucket creation is permitted only in the **Mumbai** region.  
     - Bucket creation in any other region results in an **Access Denied** error.

---

### **Task 4: Access S3 Using Third-Party Applications**
**Objective:** Use third-party applications to access S3. (Tools: S3 Browser, Cyberduck, Cloudberry Explorer, WinSCP)

**Steps:**
1. **Create an IAM User:**
   - Navigate to the AWS Management Console → IAM Service.
   - Create a new user with programmatic access.
2. **Generate Access Key and Secret Key:**
   - Download the credentials file.
3. **Configure Third-Party Tools:**
   - Open the chosen third-party application.
   - Enter the Access Key, Secret Key, and region to configure access.
4. **Validate Access:**
   - Perform operations such as uploading or downloading files.

---

#### **Task 5: Generate a Presigned URL**
**Objective:** Understand and use presigned URLs to provide temporary access to S3 objects.

**Steps:**
1. **What is a Presigned URL?**
   - A presigned URL is a temporary URL to access an S3 object without requiring authentication.
2. **Generate a Presigned URL:**
   - Use AWS Console and generate a Presigned URL
3. **Validate:**
   - Access the URL within 60 seconds and verify its functionality.

---

#### **Task 6: Restrict IAM User to Access a Specific Bucket**
**Objective:** Ensure that an IAM user can only access a designated S3 bucket.

**Requirement:**
- The user has access to their own bucket (e.g., `bucketname`, `2505-avinash`).
- Provide permissions for upload, download, and delete.

**Validate:**
   - Log in as the IAM user and verify access.

---

#### **Task 7: Restrict Specific Actions on a Bucket**
Create an IAM user.. Provide him S3FullAccess.. But on a specific bucket "Deny" him to perform "DeleteObject, DeleteBucket, PutObject, getbucketpolicy"

---

#### **Task 8: Configure S3 to Trigger SNS Notifications**
**Objective:** Set up S3 events to trigger an email notification via SNS.

**Steps:**
1. **Create an S3 Bucket:**
   - Create a bucket in the S3 console.
2. **Create an SNS Topic and Subscriber:**
   - Create a new SNS topic.
   - Add an email subscriber and confirm the subscription.
3. **Configure S3 Events:**
   - In the S3 console, go to bucket properties → Event notifications.
   - Add events for object creation and deletion.
   - Link the SNS topic.
4. **Test:**
   - Upload and delete objects to verify notifications.

---

#### **Task 9: Apply IP Restriction on Bucket Policy**
**Objective:** Restrict bucket access based on IP addresses using both IAM and bucket policies.

**Steps:**
1. **IAM Policy Approach:**
   - Create an IAM policy with IP restrictions:
2. **Bucket Policy Approach:**
   - Apply a bucket policy with IP restrictions:
3. **Test:**
   - Access the bucket from allowed and disallowed IPs to validate the restriction.

--- 



---

### **Task 1: EC2 Instance and Volume Management**  
1. Launch an EC2 instance in the **ap-south-1a** Availability Zone (AZ).  
2. Create a new **EBS volume** with a size of **1 GB** in the **ap-south-1a** AZ.  
3. Attach the volume to the EC2 instance and make it available at the operating system level.  
4. Write some data to the volume.  
5. Using the AWS Management Console, **increase the volume size to 2 GB**.  
6. Reflect the new size (2 GB) at the operating system level.  
7. Write additional data to confirm the changes.  

---

### **Task 2: Sharing EBS Volume Data Across Instances**  
1. Launch another EC2 instance in the **ap-south-2a** AZ.  
2. Transfer the data from the **2 GB volume** (attached to the instance in **ap-south-1a**) to the newly launched EC2 instance in **ap-south-2a**.  
3. Ensure the volume is made available and accessible from the **1b instance** in the new AZ.  

---

### **Task 3: Learn Amazon DLM Use Cases**  
1. Read the AWS blog article:  
   [Automating Amazon EBS Snapshot and AMI Management Using Amazon DLM](https://aws.amazon.com/blogs/storage/automating-amazon-ebs-snapshot-and-ami-management-using-amazon-dlm/).  
2. Understand the scenarios and use cases for **Amazon Data Lifecycle Manager (DLM)**.  

--- 
### AWS Task Questions Format  

---

#### **Task 1**: **Linux EC2 Instance Setup with Web Server and Custom Configuration**  
1. **Launch a Linux EC2 Instance**:  
   - Select the appropriate AMI and instance type.  
   - Configure security group rules to allow HTTP/HTTPS traffic.  
2. **Web Server Setup**:  
   - Install and configure a web server (e.g., Apache or Nginx).  
   - Add custom webpages and verify their accessibility via the public IP.  
3. **Volume Association**:  
   - Create a 2GB EBS volume.  
   - Attach the volume to the instance.  
   - Format, mount, and configure it for permanent mounting.  
4. **Golden AMI Creation**:  
   - Create an AMI of the configured instance.  
5. **Test Golden AMI**:  
   - Launch a new instance from the created AMI.  
   - Verify the web server and custom configurations are intact.  

---

#### **Task 2**: **Windows EC2 Instance Customization and Testing**  
1. **Launch a Windows EC2 Instance**:  
   - Select the appropriate AMI and instance type.  
   - Configure security group rules to allow RDP traffic.  
2. **Connect to the Instance**:  
   - Retrieve and decrypt the administrator password.  
   - Connect using an RDP client.  
3. **Perform Customizations**:  
   - Change the administrator password.  
   - Change the desktop wallpaper.  
   - Install PuTTY software.  
   - Install IIS and configure a custom webpage.  
4. **Golden AMI Creation**:  
   - Stop the instance and create an AMI.  
5. **Test Golden AMI**:  
   - Launch a new instance from the created AMI.  
   - Verify the customizations are preserved.  

---

#### **Task 3**: **Setup Password Authentication for EC2-User**  
1. Follow the steps in the provided [guide](https://comtechies.com/password-authentication-aws-ec2.html):  
   - Enable password authentication in the SSH configuration file.  
   - Restart the SSH service.  
   - Set a password for the `ec2-user`.  
2. Verify that password authentication works as expected.  

---
### **Task: Application Load Balancer with Multiple Target Groups**  

#### **Objective:**  
Create an Application Load Balancer (ALB) to deliver multiple applications using separate target groups on port 80 and port 8080.  

#### **Requirements:**  
1. **Launch EC2 Instances:**  
   - Launch **two EC2 instances**, install and configure Apache web server to serve content on **port 80**, and register them to **Target Group A**.  
   - Launch **one EC2 instance**, configure it to serve content on **port 8080**, and register it to **Target Group B**.  

2. **Create an Application Load Balancer:**  
   - Configure the ALB to route traffic based on port numbers to the corresponding target groups.  
   - Ensure the ALB has appropriate security group rules to allow HTTP traffic on both ports.  

3. **Target Group Configuration:**  
   - Target Group A should listen on **port 80** and forward requests to the two Apache instances.  
   - Target Group B should listen on **port 8080** and forward requests to the single instance.  

4. **Testing:**  
   - Access the ALB DNS name via a web browser and confirm that both applications are accessible via:  
     - `http://<ALB-DNS>` → Should serve content from the instances in Target Group A.  
     - `http://<ALB-DNS>:8080` → Should serve content from the instance in Target Group B.  

---

**Expected Deliverables:**  
- EC2 instances running and serving content.  
- ALB properly configured to forward traffic to the appropriate target groups.  
- Validation screenshots showing application accessibility through the ALB.  

---

### **AWS Task Questions Format**  

---

#### **Task 1: Configure Pipeline Mechanism Between EC2 Instances and ELB**  

**Objective:**  
Set up a load balancer to serve traffic only through the ELB, ensuring direct instance access is restricted.  

**Requirements:**  
1. **Security Group Configuration:**  
   - Modify the EC2 instance security group to allow port 80 traffic only from the ELB security group.  

2. **Access Testing:**  
   - Verify that accessing the instance directly via its IP does **not** serve the webpage.  
   - Ensure that accessing the application via the ELB DNS name works correctly.  


---

#### **Task 2: Create an Auto Scaling Group (ASG) and Set Desired Count**  

**Objective:**  
Deploy an Auto Scaling Group with a defined desired count of instances and verify its functionality.  

**Requirements:**  
1. **Auto Scaling Group Setup:**  
   - Create an ASG and set the desired capacity to **2** instances.  

2. **Verification:**  
   - Confirm that two instances are launched and running as expected.  

3. **Cleanup:**  
   - Ensure the Auto Scaling Group is deleted after testing to avoid unnecessary costs.  


---

#### **Task 3: Create an ASG Using a V1 Launch Template with Scaling Policies**  

**Objective:**  
Create an Auto Scaling Group with a launch template and configure scaling policies.  

**Requirements:**  
1. **Launch Template Creation:**  
   - Create a V1 launch template.  
   - Set the desired capacity to **2** instances.  
   - Deploy and verify the instances.  

2. **Scaling Policies:**  
   - Configure an alarm to reduce desired capacity to **1** instance when CPU utilization is ≤10%.  

3. **Scheduled Scaling:**  
   - Configure a scheduled action to increase the desired capacity to **3** instances at a specified time.  

4. **Verification:**  
   - Monitor and confirm automatic scaling behavior based on conditions and schedules.  

**Expected Deliverables:**  
- Auto Scaling Group with applied scaling policies and scheduled actions.  
- Observations on scaling adjustments based on alarms and schedules.  

---

#### * Task: Load Testing with Stress Command**  

**Objective:**  
Simulate high CPU usage on EC2 instances to observe Auto Scaling behavior.  

**Steps:**  
1. Run the stress command (Check the number of CPU cores using "nproc" command): 
 
   ```bash
   stress --cpu 1 --timeout 900
   ``` 
   
3. Observe scaling behavior based on increased load.  

**Expected Deliverables:**  
- System metrics showing CPU utilization.  
- Observations on scaling responses under load.  

---

---

### **Task 1: Launch an EC2 Instance Using CLI**
**Objective:** Launch an EC2 instance with the following parameters using the AWS CLI:  
- AMI ID  
- Instance Type  
- Subnet ID  
- Security Group ID  
- Key Pair  
- Number of instances  

**Expected Steps:**  
1. Use the `aws ec2 run-instances` CLI command.  
2. Pass all required parameters (`--image-id`, `--instance-type`, `--subnet-id`, `--security-group-ids`, `--key-name`, `--count`).  
3. Verify the instance launch by checking its status using `describe-instances`.

---

### **Task 2: Automate Web Server Setup Using User Data and S3**
**Objective:** Set up an EC2 instance as a web server, download web content (index.html and status.html) from S3, and serve it using Apache.  

**Instructions:**  
1. **Create the S3 Bucket:**  
   - Upload `index.html` and `status.html` to the bucket.  

2. **Launch EC2 Instance:**  
   - Use the below userdata to pass the following script while launching the instance:  
     ```bash
     #!/bin/bash
     yum install httpd -y
     service httpd start
     chkconfig httpd on
     //Frame the command here as a task and try.
     ```

3. Verify the setup:  
   - Access the public IP or domain of the instance to check if the web server is running and serving the files.

---

### **Task 3: Create IAM Users and Test AWS CLI Profiles**
**Objective:** Create two IAM users with specific permissions and test them using the AWS CLI.  

1. **Create IAM Users:**  
   - `user1`: Grant **S3 Full Access**.  
   - `user2`: Grant **IAM Full Access**.  

2. **Generate Access Keys:**  
   - For each user, generate the **Access Key** and **Secret Key**.  

3. **Configure CLI Profiles on Your Laptop:**  
   - Use the `aws configure --profile <profile-name>` command to set up two profiles (`user1-profile` and `user2-profile`).  

4. **Test User Permissions:**  
   - Log in using each profile:  
     - **User1:** Try creating an S3 bucket (`aws s3 mb`).  
     - **User2:** Try creating an IAM user (`aws iam create-user`).  
   - Verify that each user has the expected permissions and no access beyond what is granted.  

---

### **Task 4: Use the `aws s3 sync` Command for Incremental Updates from S3 to EC2**

**Objective:** Test incremental synchronization of web content between an S3 bucket and an EC2 instance using the `aws s3 sync` command.

**Instructions:**  
1. **Prepare the S3 Bucket:**  
   - Add the initial set of files (e.g., `index.html` and `status.html`) to your S3 bucket.  

2. **Launch an EC2 Instance and configure Web Server Setup:**  
	- use Sync command and sync data from s3 bucket to /var/www/html/ path. 

3. **Test Incremental Updates:**  
   - Add a new file (e.g., `about.html`) or modify an existing file (e.g., `index.html`) in the S3 bucket.  
   - Use the `aws s3 sync` command on the EC2 instance to pull only the updated or new files to `/var/www/html/`.  
     ```bash
     aws s3 sync s3://<bucket-name>/ /var/www/html/
     ```

4. **Verify Updates:**  
   - Access the public IP or domain of the EC2 instance in your browser to confirm that the changes are reflected on the web server.

---


### **Task 5: Automate S3 to EC2 Synchronization Using a Cron Job**

**Objective:** Set up a cron job on an EC2 instance to automate regular synchronization of web content from an S3 bucket to the web server directory.

---

**Instructions:**  
1. **Launch an EC2 Instance and Configure Web Server:**  
   - Launch an EC2 instance and install Apache:  
   - Verify that the web server is running.

2. **Set Up the Initial Synchronization:**  
   - Manually run the `aws s3 sync` command to pull the initial content from the S3 bucket (you can use task 4 web content) to `/var/www/html/`:  
     ```bash
     aws s3 sync s3://<bucket-name>/ /var/www/html/
     ```

3. **Install `crontab`:**  
   - Ensure the `cron` package is installed and enabled on your EC2 instance:  
     ```bash
     yum install cronie -y
     service crond start
     chkconfig crond on
     ```

4. **Create a Cron Job for Regular Synchronization:**  
   - Open the crontab editor:  
     ```bash
     crontab -e
     ```
   - Add the following entry to synchronize every 2 minutes:  
     ```bash
     */2 * * * * aws s3 sync s3://<bucket-name>/ /var/www/html/
     ```

5. **Test the Automation:**  
   - Add or update files in the S3 bucket and wait for the cron job to trigger.  
   - Verify that the changes are reflected on the web server by accessing the instance's public IP or domain.

---
### **Task 1: Recover a Windows EC2 Instance Administrator Password Without Key Pair**  

**Objective:** Recover the administrator password of a Windows EC2 instance if the key pair is lost using AWS Systems Manager Automation.  

**Instructions:**  
1. Navigate to the **AWS Systems Manager Console**.  
2. Choose **Run Command** from the left panel.  
3. Click **Command Document** and search for the **AWSSupport-RunEC2RescueForWindowsTool** document.  
4. Select your target Windows EC2 instance.  
5. Run the automation document and follow the instructions to reset the administrator password.  
6. Retrieve the new password and log in to the instance via RDP.  

---

### **Task 2: Make a Linux EC2 Instance a Web Server Without Logging into OS**  

**Objective:** Configure an Apache web server on an EC2 instance at launch using user data, without manual SSH access.  

**Instructions:**  
1. Launch an EC2 instance with Amazon Linux 2.  
2. Attach a user data script during instance creation to install and configure Apache:  
   ```bash
   #!/bin/bash
   yum install -y httpd
   systemctl start httpd
   systemctl enable httpd
   echo "Hello from $(hostname)" > /var/www/html/index.html
   ```  
3. Once the instance is running, access the public IP in a browser to verify the web server.  

---

### **Task 3: Change the Timezone of a Windows EC2 Instance Using SSM Run Command**  

**Objective:** Use AWS Systems Manager Run Command to change the timezone of a Windows EC2 instance.  

**Instructions:**  
1. Ensure the instance has an **SSM Agent** installed and the necessary IAM role attached.  
2. Navigate to the **AWS Systems Manager Console**.  
3. Go to **Run Command** → **Run a command**.  
4. Choose the document **AWS-RunPowerShellScript**.  
5. Select your Windows EC2 instance.  
6. Enter the following command in the script section:  
   ```powershell
   tzutil /s "India Standard Time"
   ```  
7. Click **Run Command** and verify the timezone change inside the instance.  
 

---

### **Task 4: Retrieve System Information from an EC2 Instance**  
 **Objective:** Use AWS Systems Manager Run Command to check system details like OS version, hostname, and uptime.  

 **Instructions:**  
1. Open AWS **Systems Manager Console** → **Run Command**.  
2. Choose the **AWS-RunShellScript** document for Linux or **AWS-RunPowerShellScript** for Windows.  
3. Select a target EC2 instance.  
4. Enter the following commands:  
   - **For Linux:**  
     ```bash
     uname -a
     cat /etc/os-release
     uptime
     ```  
5. Run the command and review the output.


---

### **Task 5: Change the Hostname of an EC2 Instance**  
 **Objective:** Change the hostname of an EC2 instance without logging in.  

 **Instructions:**  
- **For Linux:**  
  ```bash
  hostnamectl set-hostname NewHostname
  ```  
- **For Windows:**  
  ```powershell
  Rename-Computer -NewName "NewHostname" -Force -Restart
  ```  

---

### **Task 6: Fetch Public and Private IP Addresses of an Instance**  
 **Objective:** Use Run Command to retrieve network details of an instance.  

 **Instructions:**  
- **For Linux:**  
  ```bash
  curl http://169.254.169.254/latest/meta-data/public-ipv4
  curl http://169.254.169.254/latest/meta-data/local-ipv4
  ```  
- **For Windows:**  
  ```powershell
  Invoke-WebRequest -Uri http://169.254.169.254/latest/meta-data/public-ipv4
  Invoke-WebRequest -Uri http://169.254.169.254/latest/meta-data/local-ipv4
  ```  

---

### **Task 7: Reboot an EC2 Instance Using Run Command**  
 **Objective:** Remotely reboot an EC2 instance using Run Command.  

 **Instructions:**  
- **For Linux:**  
  ```bash
  reboot
  ```  
- **For Windows:**  
  ```powershell
  Restart-Computer -Force
  ```  
---

---

### **Task 1: Create a VPC with 2 Subnets (1 Public, 1 Private)**  
 **Objective:** Create a Virtual Private Cloud (VPC) with one public subnet and one private subnet.  

 **Specifications:**  
- **VPC:** Custom VPC  
- **Subnets:**  
  - **Public Subnet:** `ap-south-1a`  
  - **Private Subnet:** `ap-south-1b`  

 **Steps:**  
1. Create a VPC with a CIDR block (e.g., `10.0.0.0/16`).  
2. Create a public subnet in `ap-south-1a`.  
3. Create a private subnet in `ap-south-1b`.  
4. Attach an Internet Gateway (IGW) to the VPC.  
5. Update the public subnet's route table to allow internet access via IGW.  

---

### **Task 2: Create a VPC with 4 Subnets (2 Public, 2 Private)**  
 **Objective:** Set up a VPC with multiple public and private subnets for high availability.  

 **Specifications:**  
- **VPC:** Custom VPC  
- **Subnets:**  
  - **Public Subnets:** `ap-south-1a`, `ap-south-1b`  
  - **Private Subnets:** `ap-south-1a`, `ap-south-1b`  

 **Steps:**  
1. Create a VPC with a CIDR block (e.g., `10.0.0.0/16`).  
2. Create two public subnets in `ap-south-1a` and `ap-south-1b`.  
3. Create two private subnets in `ap-south-1a` and `ap-south-1b`.   


---

### **Task 3: Launch a Windows Jump Server and Connect to a Private Windows EC2 Instance**  
 **Objective:** Create a VPC and set up a Jump Server (Windows) in the public subnet to access a Windows instance in the private subnet.  

 **Specifications:**  
- **VPC:** Custom VPC  
- **Instances:**  
  - **Jump Server:** Windows AMI in Public Subnet  
  - **Private Instance:** Windows AMI in Private Subnet  

 **Steps:**  
1. Create a VPC with a public and private subnet.  
2. Launch a **Windows Jump Server** in the public subnet with an Elastic IP.  
3. Launch a **Windows EC2 instance** in the private subnet.  
4. Configure Security Groups to allow RDP from the Jump Server.  
5. Connect to the Jump Server using RDP.  
6. From the Jump Server, connect to the private Windows instance via RDP.  

---

### **Task 4: Launch a Windows Jump Server and Connect to a Private Linux EC2 Instance**  
 **Objective:** Create a VPC with a Jump Server (Windows) in the public subnet to access a Linux instance in the private subnet.  

 **Specifications:**  
- **VPC:** Custom VPC  
- **Instances:**  
  - **Jump Server:** Windows AMI in Public Subnet  
  - **Private Instance:** Amazon Linux AMI in Private Subnet  

 **Steps:**  
1. Create a VPC with a public and private subnet.  
2. Launch a **Windows Jump Server** in the public subnet with an Elastic IP.  
3. Launch a **Linux EC2 instance** in the private subnet.  
4. Configure Security Groups to allow RDP to the Jump Server and SSH from the Jump Server to the private Linux instance.  
5. Connect to the Jump Server using RDP.  
6. From the Jump Server, SSH into the private Linux instance using a key pair.  

---

### **Task 5: Launch a Linux Jump Server and Connect to a Private Linux EC2 Instance**  
 **Objective:** Set up a Jump Server (Linux) in the public subnet to access a Linux instance in the private subnet.  

 **Specifications:**  
- **VPC:** Custom VPC  
- **Instances:**  
  - **Jump Server:** Linux AMI in Public Subnet  
  - **Private Instance:** Linux AMI in Private Subnet  

 **Steps:**  
1. Create a VPC with a public and private subnet.  
2. Launch a **Linux Jump Server** in the public subnet with an Elastic IP.  
3. Launch a **Linux EC2 instance** in the private subnet.  
4. Configure Security Groups to allow SSH access from your IP to the Jump Server and from the Jump Server to the private Linux instance.  
5. SSH into the Jump Server.  
6. From the Jump Server, SSH into the private Linux instance using the key pair.  

---
### **Task 1: Test Network ACL (NACL) Rules**  
**Objective:** Understand how NACL rules affect inbound and outbound traffic by testing a web server in a public subnet.  

**Steps:**  
1. Create a **Custom VPC** with at least one **Public Subnet**.  
2. Launch an **EC2 instance** in the public subnet.  
3. Install and configure a **web server** (Apache/NGINX).  
4. Verify that the web server is accessible from the internet.  
5. Create a **new NACL** and associate it with the **public subnet** (instead of the default NACL).  
6. Try accessing the website again—it should be **blocked** due to default deny rules.  
7. Modify the NACL rules to allow **inbound HTTP (port 80) and outbound traffic**.  
8. Test again to confirm that the website is accessible.  

---

### **Task 2: Access S3 from a Private EC2 Instance Using an S3 Gateway Endpoint**  
**Objective:** Enable an EC2 instance in a private subnet to access S3 without internet connectivity.  

**Steps:**  
1. Create a **Custom VPC** with a **Private Subnet** (no internet gateway or NAT).  
2. Launch an **EC2 instance** in the private subnet.  
3. Create an **IAM Role** with **AmazonS3FullAccess** permission and attach it to the EC2 instance.  
4. From the EC2 instance, try accessing S3 using the AWS CLI (`aws s3 ls`).  
   - It should **fail** due to the lack of internet connectivity.  
5. Create an **S3 Gateway Endpoint** in the **VPC**.  
6. Modify the **private subnet's route table** to associate with the **S3 Endpoint**.  
7. Try accessing S3 again—it should now **work without internet access**.  

---

### **Task 1: Configure VPC Peering Across Different AWS Regions**  
**Objective:** Establish VPC Peering between a **Mumbai (ap-south-1)** VPC and a **Singapore (ap-southeast-1)** VPC within the same AWS account.  

**Steps:**  
1. **Create VPCs** in both **Mumbai** and **Singapore** regions.  
2. **Create Subnets** in each VPC (Public and Private as needed).  
3. **Request a VPC Peering Connection**:  
   - Navigate to the **Mumbai VPC** → **Peering Connections** → **Create Peering Connection**.  
   - Choose **Mumbai VPC as the requester** and **Singapore VPC as the accepter**.  
4. **Accept the Peering Request** from the **Singapore VPC**.  
5. **Modify Route Tables** in both VPCs to allow traffic via the peering connection.  
6. **Update Security Groups** to allow traffic between VPCs.  
7. **Test Connectivity** between resources in both VPCs using ping or other network tools.  

---

### **Task 2: Prepare a VPC Diagram**  
**Objective:** Design a **VPC architecture diagram** with:  
- **2 Public Subnets**  
- **4 Private Subnets**  
- **NAT Gateway** for private subnets to access the internet  
- **VPC Flow Logs** for monitoring


---

### **Task 1: Deploy MySQL RDS and Connect Using MySQL Workbench**  
**Objective:** Launch a **MySQL RDS** instance in a **Custom VPC’s Private Subnet** and connect using **MySQL Workbench** from a Windows EC2 instance in the public subnet.  

**Steps:**  
1. **Create a Custom VPC** with a **private and public subnet**.  
2. **Launch an RDS MySQL Instance** in the **private subnet**.  
   - Choose **MySQL** as the database engine.  
   - Ensure **public accessibility is disabled**.  
   - Set up **security groups** to allow connections from the Windows EC2 instance.  
3. **Launch a Windows EC2 instance** in the **public subnet**.  
4. **Install MySQL Workbench** on the Windows EC2 instance.  
5. **Connect to the RDS MySQL Instance** using **MySQL Workbench**.  

---

### **Task 2: Connect to MySQL RDS Using MySQL Client from a Linux Instance**  
**Objective:** Install **MySQL Client** on a Linux EC2 instance and connect to the **MySQL RDS** instance.  

**Steps:**  
1. **Launch a Linux EC2 instance** in the **Custom VPC’s Public Subnet**.  
2. **Install MySQL Client** on the EC2 instance.  
3. **Connect to the RDS MySQL instance** using the MySQL Client command-line tool.  

---

### **Task 3: Restore a Sample Database and Run SQL Query**  
**Objective:** Restore a **shared sample database** to the MySQL RDS instance and retrieve customer data using SQL.  

**Steps:**  
1. **Restore the database** using MySQL Workbench or MySQL Client.  
2. **Run an SQL command** to list customer information:  
   ```sql
   SELECT * FROM db.table;
   ```
3. **Verify the output** and ensure the database is properly restored.  

---

### **Task 4: Deploy PostgreSQL RDS and Connect Using pgAdmin**  
**Objective:** Launch a **PostgreSQL RDS** instance in a **Custom VPC’s Private Subnet** and connect using **pgAdmin** from a public EC2 instance.  

**Steps:**  
1. **Launch a PostgreSQL RDS Instance** in the **private subnet**.  
2. **Launch an EC2 instance** in the **public subnet**.  
3. **Install pgAdmin** on the EC2 instance.  
4. **Connect to the PostgreSQL RDS** instance using **pgAdmin**.  

---

### **Task 5: Deploy Microsoft SQL Server (Express) RDS and Connect Using SSMS**  
**Objective:** Launch an **MS SQL RDS (Express) instance** in a **Custom VPC’s Private Subnet** and connect using **SQL Server Management Studio (SSMS)**.  

**Steps:**  
1. **Launch an MS SQL RDS Instance** in the **private subnet**.  
2. **Launch a Windows EC2 instance** in the **public subnet**.  
3. **Install SSMS (SQL Server Management Studio)** on the Windows EC2 instance.  
4. **Connect to the MS SQL RDS instance** using **SSMS**.  

---

### **Task: Connect to a MySQL RDS Database in a Custom VPC Private Subnet Using a Local MySQL Workbench**  

**Objective:**  
- Launch a **MySQL RDS** instance in a **Custom VPC’s Private Subnet**.  
- Launch a **Linux EC2 instance** in the **Custom VPC’s Public Subnet**.  
- Ensure **network communication** between the RDS instance and the EC2 instance.  
- Install **MySQL Workbench** on your **local laptop** and connect to the RDS database via the **jump server (public EC2 instance)**.  

---

#### **Connect to MySQL RDS Using SSH Tunnel**
- Open MySQL Workbench and configure the connection:  
  - **Connection Method:** Standard TCP/IP over SSH  
  - **SSH Hostname:** `<Public_EC2_Instance_IP>`  
  - **SSH Username:** `<EC2_User>` (e.g., `ec2-user`)  
  - **SSH Key File:** Select your **EC2 key pair (.pem file)**  
  - **MySQL Hostname:** `<RDS_ENDPOINT>`  
  - **MySQL Port:** `3306`  
  - **Username:** `<DB_USER>`  

- Click **Connect** and verify database access.  

---

### **Expected Outcome:**  
- MySQL RDS is **accessible** via the **public EC2 instance** using **MySQL Workbench** on your local laptop.  
- Secure **RDS access** is achieved without exposing it **directly** to the internet.

---

Task1:  **Deploy and Test Lambda Functions**  
   - I am sharing a set of Lambda functions. Deploy them and verify their functionality:  
     - Volume Status Check  
     - Volume Encryption Check  
     - Instance Stop  
     - Instance Start  

Task 2. **S3 Event-Triggered Lambda for Instance Stop**  
   - Create an S3 bucket. When an object is uploaded to the bucket, it should trigger the **"Stop-Instance"** Lambda function, which will stop the specified EC2 instance.  

Task 3. **File Movement Based on Naming Conventions**  
   - Any file with a name starting with **"A" or "a"** should be moved to another S3 bucket.  
   - Any file with a name ending in **".bkp"** should be moved to another S3 bucket.  

Task 4. **Lambda Function for Telnet Test**  
   - Create a Lambda function to perform a **Telnet test** on `google.com` over port `443`.  
   - The function should return either **"Telnet Success"** or **"Telnet Failed"** based on the result.  

Task 5. **Inactive IAM Users - Last Login Check**  
   - Retrieve the list of IAM users who have **not logged into the AWS account in the last 24 hour**.  

Task 6. **Inactive IAM Access Keys Report**  
   - Get the list of IAM users whose **Access Key ID and Secret Access Key** have **not been used in the last 90 days**.  
   - Generate a **CSV file** with the list of such users and save it to an **S3 bucket**.  

---


Task 1. **Launch an EC2 Instance Using CloudFormation**  
   - Create a CloudFormation template to launch an EC2 instance.  
   - Deploy the template and verify that the instance is running.  

Task 2. **S3 Bucket with Lifecycle Rule**  
   - Create an S3 bucket and configure a **lifecycle rule** for managing objects.  
   - Use **ChatGPT or Former2** to generate the CloudFormation template.  
   - Modify the template to update the bucket name as needed.  
   - Deploy the template and test the lifecycle rule.  

Task 3. **EC2 Instance with Security Group and User Data (Web Server Setup)**  
   - Create a **new Security Group** within the CloudFormation template.  
   - Launch an **EC2 instance** using the same template.  
   - Use **UserData** to configure the instance as a **web server**.  
   - Open ports **80 (HTTP) and 22 (SSH) for all users (0.0.0.0/0)**.  
   - Deploy the template and verify the instance and web server setup.  

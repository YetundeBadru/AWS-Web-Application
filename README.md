# Building a Scalable Web Infrastructure by Launching an EC2 Instance in Ireland Region for SmartShop
Welcome to my project! Below are some details organized with collapsible sections.
#### 7th December, 2024.
## Table of Content
<details>
  <summary>Click to expand Table of Content</summary>

  - [Go to Introduction](#introduction)
  - [Go to Introduction](#projectobjective)
  - [Go to Introduction](#projectmission)
  - [Go to Introduction](#awsserviceutilized)
  - [Go to Introduction](#projecttask)
    - [Go to Introduction](#setUpaVirtualPrivateCloud (VPC))
    - [Go to Introduction](#setupsecuritygroups)
    - [Go to Introduction](#launchanEC2InstancewithApacheWebServer)
    - [Go to Introduction](#installapacheWebserver)
</details>
  
  ## Introduction
This is based on my experience on AWS to build a Scalable Web Infrastructure by Launching an EC2 Instance for SmartShop. SmartShop is a fictional mid-sized retail company that has recently decided to expand its business by launching an online store. As they anticipate an increase in web traﬀic due to marketing campaigns and seasonal sales, SmartShop requires a robust and reliable web infrastructure to ensure smooth customer experiences. With minimal in-house IT staﬀ and a limited budget, they seek a cost-eﬀective solution that can be manually adjusted for growth as needed, providing high availability and essential security while keeping operational complexity low.

## Project Objective 
The objective is to design and deploy a reliable web application infrastructure on AWS to:
<details>
  <summary>Click to expand Project Objective</summary>

  - Support anticipated growth with ﬂexible resource allocation
  - Ensure high availability and consistent user experience
  - Implement strong security measures to protect customer data
  - Be cost-eﬀective and optimized for performance
</details>

## Project Mission
To Develop a solution that meets SmartShop's requirements by leveraging AWS services such as EC2, Virtual Private Cloud (VPC), and Identity and Access Management (IAM).

## AWS Services Utilized
<details>
  <summary>Click to expand AWS Services Utilized</summary>

  - Amazon EC2: Hosting the scalable web application.
  - Amazon VPC: Isolating the network environment.
  - Amazon CloudWatch: Monitoring resources and setting up alerts.
  - AWS CloudTrail: Auditing AWS API calls.
</details>

## Project Tasks
1. Set Up a Virtual Private Cloud (VPC) in the Ireland Region.
- Configuring a Custom VPC to host SmartShop's infrastructure by Creating a VPC
  - In the AWS Console, go to VPC > Your VPCs > Create VPC.
  - Name the VPC, choose IPv4 CIDR block (e.g., 10.0.0.0/16), and click Create.
  - Divide the VPC into public and private subnets across multiple Availability Zones for redundancy.
- Create Subnets
  - Go to Subnets > Click "Create subnet".
  - Select your VPC, and create at least two subnets:
  - Public Subnet: CIDR- 10.0.1.0/24
  - Private Subnet: CIDR- 10.0.2.0/24
  - Name them clearly for easy identification.
![image](https://github.com/user-attachments/assets/dc7812bd-1d98-484a-836f-88d18f26770d)

2. Set Up Security Groups in the Ireland Region
- Go to EC2 Instance > Security Groups > Create Security Group
- Input Basic Details
  - Name your Security Group
  - Description: Allow SSH and HTTP traffic.
  - Select VPC (The VPC that was created)
  ![Screenshot 2024-12-12 162158](https://github.com/user-attachments/assets/5bdecc4b-271e-4a77-8ecd-36f43946765a)
- Set Up Inbound rules
  - Click on "Add rule"
  - Type: SSH and HTTP
  - Source: Allow inbound HTTP from anywhere and SSH access from your IP for the web and admin access
  ![Screenshot 2024-12-12 162454](https://github.com/user-attachments/assets/5e485aaa-6bec-4284-9a75-2c60d1e506b3)
- Set Up Outbound rules
  - Click on "Add rule"
  - Type: Allow all traffic to go anywhere
  - Source: Custom
  ![Screenshot 2024-12-12 162616](https://github.com/user-attachments/assets/69e421b6-aaaa-4ff7-a428-bb47f711493e)
- Click on Create Security Group.
  - Here is the Security Group created
![Screenshot 2024-12-12 162835](https://github.com/user-attachments/assets/0d0a0f65-9159-4a4e-bc23-00afa367368c)

3. Launch an EC2 Instance with Apache Web Server in the Ireland Region
- Go to EC2 Instance > Instances > Launch Instances
- Name your Instance
![Screenshot 2024-12-12 165916](https://github.com/user-attachments/assets/e17965c4-743c-4529-807f-82fcfe187012)
-Choose an appropriate Amazon Machine Image (AMI) for the SmartShop web server (Amazon Linux 2 AMI (HVM)
![Screenshot 2024-12-12 170026](https://github.com/user-attachments/assets/754a6f39-201c-490d-b52e-e062aea776dd)
![Screenshot 2024-12-12 170100](https://github.com/user-attachments/assets/03f19be7-71e4-4572-b627-ee3eb1929af9)
- Select Instance Type (t2.micro)
![Screenshot 2024-12-12 170230](https://github.com/user-attachments/assets/a3940e2c-fedf-486d-893d-120f56c063d1)
- Click Create Key Pair.
   - Provide a name for your key pair (e.g., MyKeyPair).
   - Choose the Key Pair Type: RSA (default)
   - Click Create Key Pair.
   - The private key file (.pem ) will be downloaded automatically to your computer
   - Save it securely; it cannot be downloaded again
![Screenshot 2024-12-12 170550](https://github.com/user-attachments/assets/090b1191-0654-400c-8a24-1514f01417a3)
- Choose Keypair Login (The one that was created)
![Screenshot 2024-12-12 170735](https://github.com/user-attachments/assets/fb4b2046-2ef8-46e3-8103-fb9833ffb380)
- Configure Network settings
  - click the “Edit” button
  - Select the VPC earlier created
  - Select the Public Subnet earlier created
  - Make sure the “Auto-assign Public IP” is set to “Enabled”
  - Select the security group that was earlier created.
![Screenshot 2024-12-12 190120](https://github.com/user-attachments/assets/52074274-1f56-4ced-a2e4-cd2a95c80a9d)
- Configure Storage
   - Leave the “Configure storage” at 8gb
![Screenshot 2024-12-12 190200](https://github.com/user-attachments/assets/d4bc2997-57e6-43ae-a94c-b66970c92e53)
- Review your configuration summary and then click the “Launch Instance”
![Screenshot 2024-12-12 190257](https://github.com/user-attachments/assets/2e060d42-ba43-4f3b-8e95-3ee2b4762251)
- Instance is ready when you see “2/2 check passed” (it might take a few minutes)
![Screenshot 2024-12-12 190356](https://github.com/user-attachments/assets/f79c88c8-9f36-4f74-b354-32c06d8bd1cf)

4. Install Apache Web Server
- Click on the Instance created and SSH into it.
  - Go to EC2 Instance > Instances > Connect to Instance
![image](https://github.com/user-attachments/assets/8091a9d5-7427-44c9-a933-56b66881b1ad)
  - Click on "SSH Client"
![image](https://github.com/user-attachments/assets/78db741e-619d-4d16-b4e1-5dfd2f996ec6)
- SSH into the instance:
  - Go to the location where you downloaded your keypair on your Local Device
  - Right-click on any space and select the “git bash or Command prompt”
![image](https://github.com/user-attachments/assets/edd639ea-e8d8-4e90-af19-8ccd0e5c2c99)
- Enter the below code in the new window opened
     ssh -i "your-key.pem" ec2-user@<public-ip>
![Screenshot 2024-12-08 172341](https://github.com/user-attachments/assets/897167ce-6158-462b-8851-3862da43771f)
- Run the following commands to install Apache:
  sudo yum update -y
  sudo yum install httpd -y
  sudo systemctl start httpd
  sudo systemctl enable httpd
![Screenshot 2024-12-08 172544](https://github.com/user-attachments/assets/1c290ce5-b4a7-4f96-b11a-a0bbb90f90be)
![Screenshot 2024-12-08 172621](https://github.com/user-attachments/assets/29de9e49-0ee9-4008-8ef0-c60520ffc906)
![Screenshot 2024-12-08 172700](https://github.com/user-attachments/assets/57f65a8d-29da-431e-a0da-87413ad3131b)
![Screenshot 2024-12-08 172722](https://github.com/user-attachments/assets/bc93180e-7ccd-47db-8196-5b75562abd2a)
- Confirm Apache is running by visiting the instance’s public IP address in a browser.
![image](https://github.com/user-attachments/assets/a1f872d8-ac71-4768-ba77-cc9f5414a56d)
- Copy the public IP address of your instance into any browser
![Screenshot 2024-12-08 172956](https://github.com/user-attachments/assets/b9843ae1-7300-4121-97fd-b8a689ab8843).

### Apache is successfully installed in your browser !!!

## Author
#### YETUNDE BADRU


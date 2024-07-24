# Create-an-Internet-Gateway-and-NAT-Gateway-with-Route-Table-in-VPC
Here, i am creating AWS VPC setup from scratch 
In this mini project, i will create an Internet Gateway, a NAT Gateway, and configure route tables for a public
subnet and a private subnet within an Amazon VPC using the AWS Management Console.

VPC Overview Design

![image](https://github.com/user-attachments/assets/5167ca20-593e-4b74-a9cc-427952bb2828)

# Set Up

## Step 1 - Create the VPC 

1. Login to AWS MManagement Console and navigate to VPC service
2. Click on "Your VPCs" on the left-hand panel
3. Click "Create VPC" button in the top right hand corner
4. Let's name the VPC "Demo VPC"
5. Set the IPv4 CIDR block to 10.0.0.0/16 (that's 65,536 IP Addresses we are assigning to our VPC)
6. Leave all other things the same and click "VPC" at the bottom right hand corner. DONE

   <img width="530" alt="image" src="https://github.com/user-attachments/assets/21e43f0b-2e03-405f-85de-f9bf825bd799">

## Step 2 - Create the Subnet
I am creating 4 subnets - 2 Public Subnets in separate Availability Zone (AZ) and 2 Private Subnets in the same separate AZs
 1. Opened the VPC console
 2. Clicked on "Subnets" on the left-hand panel
 3. Clicked "Create subnet" button in the top right hand corner
 4. Clicked the drop down and selected the VPC named "Demo VPC" created in Step 1
 5. Named Subnet 1 "Public Subnet A"
 6. Choose an AZ "a" for whatever region closest. For example: "us-east-1a"
 7. Set the IPv4 CIDR block to 10.0.0.0/24 [10.0.0.0 - 10.0.0.255] (that's 256 IP addresses)
 8. Then clicked the button "Add new subnet" at the bottom left hand corner. I completed similar steps shown in 5-7 for the other 3 subnets created.
 9. Named Subnet 2 "Public Subnet B", Choose AZ "b", Set the IPv4 CIDR block to 10.0.1.0/24 [10.0.1.0 - 10.0.1.255], clicked "Add new subnet" at the bottom left hand corner
10. Named Subnet 3 "Private Subnet A", Choose AZ "a" (same AZ as Subnet 1), Set the IPv4 CIDR block to 10.0.16.0/20 [10.0.16.0 - 10.0.31.255] (that's 4096 IP addresses), 
    clicked "Add new subnet" at the bottom left hand corner
11. Named Subnet 4 "Private Subnet B", Choose AZ "b" (same AZ as Subnet 2), Set the IPv4 CIDR block to 10.0.32.0/20 [10.0.32.0 - 10.0.47.255]
12. Clicked the "Create subnet" button in the bottom right hand corner. DONE

<img width="631" alt="image" src="https://github.com/user-attachments/assets/fbfbf41b-2438-4484-88be-33b99cf90d6f">

## Step 3 - Create Internet Gateway and Route Table
   Create Internet Gateway

1. Opened the VPC Console
2. Clicked on "Internet gateways" on the left-hand panel
3. Clicked "Create internet gateway" button in the top right hand corner
4. Named the internet gateway "Demo Internet Gateway"
5. Clicked "Create internet gateway" in the bottom right hand corner. DONE

<img width="924" alt="image" src="https://github.com/user-attachments/assets/b31bba48-be67-447e-8900-6158eaf832ab">

Attached the Internet Gateway to "Demo VPC"

1. Went back to the internet gateway dashboard

2. Selected the newly created internet gateway called "Demo Internet Gateway"

3. Clicked the "Actions" dropdown button at the top right hand corner and click "Attach to VPC"
   ![image](https://github.com/user-attachments/assets/661f55e0-064d-4cb6-9f8a-1a99b2fbdd88)

## Create the Route Tables

A default route table has already been created for my created VPC. However, I will not use the default route table associated with that VPC. I will create 3 route tables of my own (Public Route Table, Private Route Table A, Private Route Table B)

1. Opened the VPC Console
2. Clicked on "Route tables" on the left-hand panel
3. Clicked "Create route table" button in the top right hand corner
4. Named the 1st route table "Public Route Table", select "Demo VPC", click "Create route table" button at the bottom right hand corner.

    Public Route Table
   ![image](https://github.com/user-attachments/assets/5b51d1c9-02c3-469b-866b-d1aef9e6d1a6)

5. Named the 2nd route table "Private Route Table A", select "Demo VPC", click "Create route table" button at the bottom right hand corner.

   Private Route Table A
   <img width="735" alt="image" src="https://github.com/user-attachments/assets/372f5403-8cff-44b0-8565-a502d1c53db5">

6. Named the 3rd route table "Private Route Table B", select "Demo VPC", click "Create route table" button at the bottom right hand corner. DONE

   Private Route Table B
   <img width="890" alt="image" src="https://github.com/user-attachments/assets/af4daf04-d5c3-4475-a40a-d2f02d517dc7">

Assign Subnets to Route Tables 

Assign Public Subnets to "Public Route Table"

1. Went back to the route tables dashboard

2. Selected "Public Route Table"

3. Clicked the "Actions" dropdown button at the top right hand corner and clicked "Edit subnet associations"

   ![image](https://github.com/user-attachments/assets/cb13de3c-f6cc-4def-9784-2c3b38f36a7b)
Assign Private Subnet to "Private Subnet A"

1. Back to the route tables dashboard
2. Selected "Private Route Table A"
3. Clicked the "Actions" dropdown button at the top right hand corner and clicked "Edit subnet associations"
4. Selected "Private Subnet A" and clicked "Save associations" button at the bottom right hand corner

   ![image](https://github.com/user-attachments/assets/86a3c146-e3de-46e3-83a9-c7402ea03405)

Assign Private Subnet to "Private Subnet B"

1. Back to the route tables dashboard
2. Selected "Private Route Table B"
3. Clicked the "Actions" dropdown button at the top right hand corner and clicked "Edit subnet associations"
4. Selected "Private Subnet B" and click "Save associations" button at the bottom right hand corner DONE

![image](https://github.com/user-attachments/assets/492ed4e4-08d0-4339-86ee-c47442b62b8b)

Update Public Route Table to make "Public Subnet A" and "Public Subnet B" Public

1. Back to the route tables dashboard
2. Selected "Public Route Table"
3. Clicked the "Actions" dropdown button at the top right hand corner and clicked "Edit routes"
4. Clicked "Add route", for Destination route select "0.0.0.0/0", for Target select "Internet Gateway" and select "Demo Internet Gateway", click "Save changes" button at 
   the bottom right hand corner. DONE

![image](https://github.com/user-attachments/assets/f3457638-5455-4cc2-921e-69937ba30dbc)

Step 4 - Create NAT Gateway (NATGW)
For high availability i will create 2 NATGW. One in each AZ (One in Public Subnet A and One in Public Subnet B)

1. Opened the VPC Console
2. Clicked on "NAT gateways" on the left-hand panel
3. Clicked "Create NAT gateway" button in the top right hand corner
4. Named the 1st NATGW "NATGW A", Select "Public Subnet A" that we created in a previous step, click "Allocate Elastic IP" button, and click "Create NAT gateway" button in 
   the bottom right hand corner

![image](https://github.com/user-attachments/assets/8c0a33cf-78cb-4376-8db3-4202b7b9d4c5)
![image](https://github.com/user-attachments/assets/3773417a-e558-41fc-8cb4-c35fbd33de54)

5. Backed to the NATGW dashboard and clicked "Create NAT gateway" button in the top right hand corner
6. Named the 2nd NATGW "NATGW B", Select "Public Subnet B" that we created in a previous step, click "Allocate Elastic IP" button, and click "Create NAT gateway" button in 
   the bottom right hand corner DONE

![image](https://github.com/user-attachments/assets/ba501e19-097f-4c6b-8e3b-d635d00d6e61)


Connect Route Tables to NATGW

1. Opened the VPC Console
2. Clicked on "Route tables" on the left-hand panel
3. Selected "Private Route Table A"
4. Clicked the "Actions" dropdown button at the top right hand corner and click "Edit routes"
5. Clicked "Add route", for Destination route select "0.0.0.0/0", for Target select "NAT Gateway" and select "NATGW A", click "Save changes" button at the bottom right hand 
   corner.

![image](https://github.com/user-attachments/assets/2d8710d9-cb35-492b-8c75-db3fb63c040a)

1. Back to the Route tables dashboard
2. Selected "Private Route Table B"
3. Clicked "Actions" dropdown button at the top right hand corner and click "Edit routes"
4. Clicked "Add route", for Destination route select "0.0.0.0/0", for Target select "NAT Gateway" and select "NATGW B", click "Save changes" button at the bottom right hand corner. DONE

![image](https://github.com/user-attachments/assets/c1f112d5-9500-4795-a620-93468a5b6696)

NOTE: The default NACL allows all inbound and all outbound. We will not change the default NACL settings in this lab. Found in VPC console.

NACL Inbound Rules

<img width="732" alt="image" src="https://github.com/user-attachments/assets/7ac2753b-ad4a-41f4-80c2-8bd6db96585f">

NACL Outbound Rules

<img width="722" alt="image" src="https://github.com/user-attachments/assets/dd9cb49f-2159-4eca-afde-94bab6f26037">

Step 5 - Create Bastion Host
Note: For high availability, it would be best to have one bastion host in each AZ. However, for simplicity, we will only create one Bastion Host - located in Public Subnet A (as shown in the "VPC Architecture Design" at the beginning of this ReadMe

1. Inside the EC2 console
2. Clicked "Instances" on the left-hand panel
3. Clicked "Launch instances" button in the top right hand corner
4. Named the instance "Bastion Host"
5. Kept AMI as Linux, Keep architecutre 64-bit(x86), Kept instance type t2 micro (to stay within the free tier)
6. Key Pair: Selected "Proceed without a key pair (Not recommended)" In this lab i will be using the EC2 Connect to SSH into our instance and to test the architecture. 
   Thus, i will not need a key pair here. However, if you i want to further secure my instance and if i use my SSH client then a key pair will be needed.
7. Edited Network Settings: Change the Default VPC to "Demo VPC", Change subnet to "Public Subnet A", Enable auto-assign public IP.
8. Edit Security Group (SG): Select "Create security group", name the SG "BastionHostSG", Description:"Security group for Bastion Host" (Optional), Allow SSH from anywhere, 
   0.0.0.0/0
9. Click "Launch instance" button at the bottom right hand corner DONE

![image](https://github.com/user-attachments/assets/d7b1f5f1-0090-4184-bc74-0d4d5db21d22)
![image](https://github.com/user-attachments/assets/cba432cd-af58-408d-8088-ce6a8bc28fcb)
![image](https://github.com/user-attachments/assets/06b5f9ec-1bbc-43a0-8879-660e0682fbe0)
![image](https://github.com/user-attachments/assets/9698a936-42d1-4ca5-945f-f5e3a5fa3252)
![image](https://github.com/user-attachments/assets/1f35d949-f528-446b-9273-bdb81230806b)
![image](https://github.com/user-attachments/assets/afcc5dd4-b161-4d3a-8013-4ad7b5367f12)

# Step 6 - Create Private EC2 Instances
Create Private Insance in Private Subnet A

1. Back to the EC2 console
2. Clicked "Launch instances" button in the top right hand corner
3. Named the instance "Private Instance A"
4. Kept AMI as Linux, Keep architecutre 64-bit(x86), Keep instance type t2 micro (to stay within the free tier)
5. Key Pair: Click "Create new key pair", Name the keypair "VPCKeyPair", keep everything else default and click "Create key pair" button at the bottom right hand corner - 
   the private key pair file will be downloaded to your computer. Make sure to store this file in a known place on your computuer. We will have to use the contents in this 
   file a later step

![image](https://github.com/user-attachments/assets/cf9af625-d561-432d-8337-f52a61ab21c5)

1. Edited Network Settings: Change the Default VPC to "Demo VPC", Change subnet to "Private Subnet A", DO NOT enable auto-assign public IP (this is our private instance and 
   it should not have a public IP address)
2. Edited Security Group (SG): Select "Create security group", name the SG "PrivateInstanceSG", Description: "Security group for private instance A and private instance B" 
   (Optional), Allow SSH from Custom: Select the SG of the Bastion Host
3. Click "Launch instance" button at the bottom right hand corner DONE

   ![image](https://github.com/user-attachments/assets/8ae80f8b-ea71-4901-ac6b-e94498a0caaa)

   ![image](https://github.com/user-attachments/assets/bbec4cb2-50f6-4b0d-83d3-27d0a6992737)


# Create Private Instance in Private Subnet B

1. Back to the EC2 console
2. Clicked "Launch instances" button in the top right hand corner
3. Named the instance "Private Instance B"
4. Kept AMI as Linux, Keep architecutre 64-bit(x86), Keep instance type t2 micro (to stay within the free tier)
5. Key Pair: In the dropdown select the keypair "VPCKeyPair"
6. Edited Network Settings: Change the Default VPC to "Demo VPC", Change subnet to "Private Subnet B", DO NOT enable auto-assign public IP (this is our private instance and 
   it should not have a public IP address)
7. Edited Security Group (SG): Click "Select existing security group", Select the "PrivateInstanceSG" SG,
8. Clicked "Launch instance" button at the bottom right hand corner DONE

![image](https://github.com/user-attachments/assets/f20129ec-a806-4900-a3ef-ef4da6200734)
![image](https://github.com/user-attachments/assets/bef057d9-a471-4253-beac-88ed6543d991)
![image](https://github.com/user-attachments/assets/fd795bca-5435-45f0-b2a6-8519af61464b)


Test System
We are going to test our infrastructure to make sure we can properly SSH into our Bastion host and our private EC2 instances. We will also make sure our Bastion host and our private instances have access to the internet via the route tables, the internet gateway, and the NAT gateway (private instances only)

# Step 7 - SSH into Bastion Host and into Private Instances to Test Connectivity
1. SSH into our Bastion Host using EC2 Connect

EC2 connect is an AWS feature that allows us to easily and securely SSH into our instances without the need of an external SSH client like Putty

1. Open the EC2 console
2. Select the "Bastion Host"
3. Click the "Connect" button at the top right of the page

![image](https://github.com/user-attachments/assets/a1b9ddf7-9719-4742-9e6f-3c9a8b9e0f58)

4. Clicked "Connect" button at the bottom right of the screen

   ![image](https://github.com/user-attachments/assets/577c29da-31ed-451e-90ff-e55256fe6bb4)
   ![image](https://github.com/user-attachments/assets/a79536c9-1b50-4971-831b-31292c8e7f4d)

   ![image](https://github.com/user-attachments/assets/b87431c1-14b7-4c1d-abc4-be4d3c240243)

5. If you get a screen like the one below then you have successfully SSH into your Bastion host DONE

<img width="497" alt="image" src="https://github.com/user-attachments/assets/08b45449-029b-4e13-8867-af7cb5242bd6">


2. Test if the Bastion Host has access to the internet

1. Type "ping www.google.com" and hit Enter into the terminal window. You should receive feedback as shown in the screen shot below.
2. Make sure to hold Ctrl and press "C" to stop the ping.
3. If your outcome is similar to what's shown below then your Bastion host has access to the internet DONE

<img width="567" alt="image" src="https://github.com/user-attachments/assets/4d44b509-7e8f-4f6d-bd3a-737dbe08c33b">



3. SSH into Private Instance A from our Bastion Host

1. Type "nano VPCKeyPair.pem" and hit Enter (nano command allows us to create and store a text file within the terminal. We need to upload our VPCKeyPair so we can 
   reference it when we SSH into the Private Instance)
2. Go to the VPCKeyPair.pem file saved on your computer. Open it. Copy ALL the content. Paste it into the terminal (hint hold ctrl and shift and press "v")

<img width="447" alt="image" src="https://github.com/user-attachments/assets/d48c6124-1c77-48cc-b855-c38ef22553f2">

3. Hold ctrl and press "X" to exit. Save the content by press Y for yes. Then press "Enter".
   Our uploaded VPCKeyPair.pem text file is formated for others to access it (current chmod access code is 644 - "chmod 644"). It is required that your private key files 
   are NOT accessible by others. Therefore, we must change the access permissions for only us to have access ("chmod 400"). For that we will use the "chmod" command

4. Type "chmod 400 VPCKeyPair.pem" and press Enter. This remove access for others and only allows read access to us.

5. In a seperate tab, go to the EC2 console

6. Select "Private instance A" and copy the private IP address as shown in the screenshot below. We will need to reference this IP address to SSH into it. Go back to the 
   EC2 Connect Window terminal.

   ![image](https://github.com/user-attachments/assets/b6690749-5f3c-49be-b2c4-5b5e2eff753d)

   Now we are ready to SSH into our Private Instance A via our Bastion host by using our keypair

7. Type "ssh ec2-user@INSERT YOUR PRIVATE IP ADDRESS YOU JUST COPIED -i VPCKeyPair.pem". Hit Enter. As an example Your code should look like this (your IP address will be 
   different): "ssh ec2-user@10.0.19.224 -i VPCKeyPair.pem"

8. A prompt will come up asking if your are sure you want to connect. Type "yes" and you should have successfully SSH into your Private Instance A via your bastion host. 
   DONE

  ![image](https://github.com/user-attachments/assets/6f025174-8b28-4615-9bb6-71e68a4ee6a8)


4. Test if Private Instance A has access to the internet

1. Type "ping www.google.com" and hit Enter into the terminal window. You should receive feedback as shown in the screen shot below.
2. Make sure to hold Ctrl and press "C" to stop the ping.
3. If your outcome is similar to what's shown below then your Bastion host has access to the internet DONE

   <img width="590" alt="image" src="https://github.com/user-attachments/assets/c0cc75a5-a28e-4973-bc9b-e17d0467da07">

   

  



   


























   


   



   

   

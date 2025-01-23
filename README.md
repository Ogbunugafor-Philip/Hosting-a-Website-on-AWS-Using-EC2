# Hosting-a-Website-on-AWS-Using-EC2


## Introduction
This project aims to demonstrate the fundamental concepts of cloud computing by hosting a simple website on Amazon Web Services (AWS). It involves deploying an EC2 instance, configuring security settings with security groups, and optimizing the instance's performance using an EC2 placement group. The project will guide you through the process of setting up a secure and scalable web server environment while ensuring the website is accessible to users over the internet. By the end of this project, you will have a clear understanding of how to use AWS services to deploy and manage a basic website securely.

## Objectives
- Deploy an EC2 instance on AWS to host a basic website.
- Configure a security group that ensures secure and restricted access to the instance.
- Utilize an EC2 placement group for performance optimization and low latency.
- Host a static webpage and verify its accessibility via the public IP address.

## Project Steps

### Step 1: Create an EC2 Placement Group
1. Navigate to the AWS Management Console.
2. Go to **EC2 Dashboard > Placement Groups**.
3. Create a new placement group with the Cluster strategy to ensure low latency and high throughput (you can choose another strategy based on your needs).

### Step 2: Configure a Security Group
1. Go to **EC2 Dashboard > Security Groups**.
2. Create a new security group:
   - Allow HTTP (port 80) traffic from anywhere (0.0.0.0/0) to enable website access.
   - Allow SSH (port 22) traffic only from your IP address for administrative access.
3. Save the security group.

### Step 3: Launch an EC2 Instance
1. Go to **EC2 Dashboard > Instances** and click **Launch Instances**.
2. Choose Ubuntu as the operating system.
3. Select an instance type (e.g., t2.micro for free tier eligibility).
4. In the **Advanced Details** section, select the placement group you created earlier.
5. Assign the security group created in Step 2 to the instance.
6. Launch the instance.

### Step 4: SSH into the EC2 Instance
1. Open your terminal.
2. Locate your private key file. The key used to launch this instance is `solution_architect.pem`.
3. Run this command to ensure your key is not publicly viewable:
   ```bash
   chmod 400 solution_architect.pem
   ```
4. Connect to your instance using its Public DNS:
   ```bash
   ssh -i "solution_architect.pem" ubuntu@ec2-54-224-167-105.compute-1.amazonaws.com
   ```

### Step 5: Install and Configure a Web Server
1. Update the package index to ensure you get the latest versions:
   ```bash
   sudo apt update -y
   ```
2. Upgrade installed packages to their latest versions:
   ```bash
   sudo apt upgrade -y
   ```
3. Install Apache web server:
   ```bash
   sudo apt install apache2 -y
   ```
4. Start the Apache service immediately:
   ```bash
   sudo systemctl start apache2
   ```
5. Configure Apache to start automatically when the system boots:
   ```bash
   sudo systemctl enable apache2
   ```
6. To confirm that the webserver is running correctly, copy your EC2 public IP address and paste it into your browser.

### Step 6: Host a Website
1. Download a website template from [BootstrapMade](https://bootstrapmade.com/):
   ```bash
   wget {template link}
   ```
2. View the template to ensure a successful download:
   ```bash
   ls
   ```
3. Unzip the template:
   ```bash
   unzip {template name}
   ```
4. Navigate to the template folder:
   ```bash
   cd {template folder name}
   ```
5. Copy everything in the template folder to `/var/www/html/`:
   ```bash
   sudo mv * /var/www/html/
   ```
6. Restart Apache:
   ```bash
   sudo systemctl restart apache2
   ```

### Step 7: Test the Website
1. Obtain the public IP address of your EC2 instance from the AWS Management Console.
2. Open a browser and enter the public IP address.

## Conclusion
In this project, we successfully deployed a basic website on AWS using an EC2 instance, secured it with a custom security group, and optimized its performance through the use of an EC2 placement group. By following these steps, we ensured the website was both accessible and secure, with controlled traffic access and minimized latency. This project not only demonstrated the core capabilities of AWS but also provided hands-on experience in configuring essential cloud services. With this knowledge, you are now equipped to deploy and manage scalable, secure applications on AWS in future projects.


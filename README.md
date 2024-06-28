# Deploying a Static Website on AWS EC2 Instance
This guide provides step-by-step instructions to deploy a static website on an AWS EC2 instance.

## Prerequisites
Before starting, ensure you have:

- An AWS account
- Basic knowledge of AWS EC2
- SSH client installed on your local machine
## Step 1: Launch an EC2 Instance
- Login to AWS Management Console:

Navigate to AWS Management Console.
- Launch an EC2 Instance:

### Go to the EC2 Dashboard.
    - Click on "Launch Instance."
    - Choose an Amazon Machine Image (AMI). For this tutorial, select Amazon Linux 2 AMI (HVM), SSD Volume Type.
    - Choose an Instance Type. The t2.micro type is eligible for the free tier.
    - Configure Instance Details (you can leave the default settings).
    - Add Storage (you can leave the default settings).
    - Add Tags (optional).
    - Configure Security Group:
    - Add a rule to allow HTTP traffic.
    - Ensure SSH traffic is allowed from your IP.
### Launch and Connect:

-   Review and launch the instance.
-   Download the key pair (.pem file) and keep it safe.
-   Connect to the instance using SSH:
```bash
ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-public-dns
```

## Step 2: Install and Configure a Web Server
- Update the package repository:

```bash
sudo yum update -y
```
- Install Apache (HTTPD):

```bash
sudo yum install -y httpd
```
- Start the Apache service:

```bash
sudo systemctl start httpd
```
- Enable Apache to start on boot:

```bash
sudo systemctl enable httpd
```

## Step 3: Deploy Your Static Website
- Upload your website files:

- Move your website files to the web server's root directory:

```bash
sudo mv /home/ec2-user/your-website-files/* /var/www/html/
```
- Set the correct permissions:

```bash
sudo chown -R apache:apache /var/www/html
```
## Step 4: Verify the Deployment
- Access your website:
Open a web browser and navigate to http://your-ec2-public-dns.
You should see your static website displayed.

## Troubleshooting
- Permission Denied: Ensure your .pem file has the correct permissions:

```bash
chmod 400 /path/to/your-key-pair.pem
```
- HTTP Error 403 (Forbidden): Check the permissions of the files in /var/www/html:

```bash
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html
```
- Cannot Connect to EC2 Instance: Ensure your security group allows incoming SSH (port 22) and HTTP (port 80) traffic.

Conclusion
You have successfully deployed a static website on an AWS EC2 instance. For more advanced setups, consider using services like AWS S3 for static site hosting, AWS CloudFront for CDN, and configuring domain names with Route 53.

By following this guide, you should have your static website up and running on an AWS EC2 instance. For any further questions or improvements, feel free to contribute or open an issue.

License
This project is licensed under the MIT License. See the LICENSE file for details.

# Host-CV-on-Ubuntu-EC2
Deploying a GitHub Repository to an EC2 Instance with CI/CD Automation
Introduction
This guide walks you through setting up an AWS environment, configuring GitHub secrets, and automating deployment using GitHub Actions. This process is commonly used for hosting websites, deploying applications, and managing infrastructure as code. By integrating GitHub with EC2, you can streamline deployments and maintain consistency.
Step-by-Step Guide
1. Set Up a VPC with a Public Subnet
•	Create a Virtual Private Cloud (VPC) with a public subnet.
•	Ensure your VPC has DNS resolution enabled to allow hostname resolution.
•	Set up an Internet Gateway (IGW) and attach it to the VPC to allow internet access.
2. Configure Security Group (SG) and Network ACLs (NACLs)
•	Create a Security Group (SG) and Network ACLs (NACLs) to allow traffic on the necessary ports: 
o	SSH (22) – For remote access.
o	HTTP (80) – For web traffic.
o	HTTPS (443) – For secure web traffic.
3. Launch an EC2 Instance
•	Choose an Amazon Linux or Ubuntu instance.
•	Attach a key pair (.pem file) for SSH authentication.
•	Assign a public IP address to enable external access.
4. Set Up a GitHub Repository
•	Create a GitHub account (if you don’t have one).
•	Create a new repository and include a README file.
5. Upload Files to the GitHub Repository
•	Add files such as your CV, HTML, CSS, or any content you want to host.
•	You can either use Git commands to push the files from local to Github or upload

6. Add EC2 Variables to GitHub Secrets
•	Navigate to your repository’s Settings > Secrets and variables > Actions.
•	Click "New repository secret" and create the following secrets:
Secret Name	Value
EC2_SSH_KEY	Contents of your .pem key file
HOST_DNS	Public DNS of your EC2 instance
USERNAME	Default username (e.g., ec2-user for Amazon Linux, ubuntu for Ubuntu)
TARGET_DIR	Default directory (e.g., /home/ubuntu)
•	Note: The secret names should match those referenced in your GitHub Actions workflow YAML file.

7. Create a GitHub Actions Workflow
•	Inside your GitHub repository, create the following directory and file: 
/.github/workflows/deploy.yml

Or do manually 


•	Add a YAML workflow file containing the automation script to deploy your repository to EC2. https://github.com/synthetico/Host-CV-on-Ubuntu-EC2.git
8. Configure the YAML Workflow
•	Retrieve the necessary GitHub Actions workflow code from a reference repository.
•	https://github.com/synthetico/Host-CV-on-Ubuntu-EC2.git 
•	Modify the YAML file, ensuring the secret names match those set in GitHub Secrets.
•	If you understand YAML, you can fully customize the deployment script to fit your needs.
9. Run the Workflow and Monitor for Errors
•	Push the YAML file to GitHub and trigger the workflow by committing a change.
•	Monitor the execution under GitHub Actions > Workflows in your repository.
10. Verify Deployment
•	Copy and paste the EC2 public DNS into a browser to check if the hosted content is accessible.
Optional: Use an ALB, ASG, and Custom DNS
•	To improve scalability and reliability, you can: 
o	Attach your EC2 instance behind an Auto Scaling Group (ASG).
o	Use an Application Load Balancer (ALB) for traffic distribution.
o	Replace the EC2 DNS with a custom domain name for a professional setup.


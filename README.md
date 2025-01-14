# AWS High-Availability Nginx Infrastructure with Terraform (IaC)

## Project Overview
This project provisions a highly available Nginx infrastructure on AWS using Terraform. It includes:

- **VPC**: A custom Virtual Private Cloud with CIDR block `172.16.0.0/16`.
- **Subnets**: Two public subnets in different availability zones.
- **Internet Gateway**: For public internet access.
- **Application Load Balancer (ALB)**: To distribute traffic across Nginx instances.
- **Auto Scaling Group (ASG)**: Ensures high availability with a minimum of two Nginx instances.
- **Security Groups**: Configured for HTTP traffic.
- **Amazon S3 Bucket**: For storage.

## Prerequisites

1. **Terraform**
   - Run the following command to check your version:
     ```bash
     terraform version
     ```
   - If you dont have Terraform on your system or your version is outdated, update it (e.g., using Chocolatey on Windows):
     ```powershell
     choco install terraform --pre
     ```

2. **AWS Credentials**
   - Obtain your AWS Access Key ID and Secret Access Key.

3. **Git**
   - Ensure Git is installed to clone the repository.

4. **AWS CLI (optional)**
   - Install and configure the AWS CLI for additional troubleshooting.

## Getting Started

1. **Clone the Repository**
   ```bash
   git clone https://github.com/ArashMHD91/terraform-aws-ha-nginx.git
   cd terraform-aws-ha-nginx
   ```

2. **Export AWS Credentials**
   Configure your AWS credentials as environment variables:
   ```bash
   export AWS_ACCESS_KEY_ID="your-access-key-id"
   export AWS_SECRET_ACCESS_KEY="your-secret-access-key"
   ```

3. **Review and Customize Variables**
   Edit the `variables.tf` file to customize the configuration as needed:
   - **Region**: Update `aws_region` to your desired AWS region.
   - **AMI ID**: Replace `ami_id` with the latest Ubuntu AMI ID for your region.
   - **S3 Bucket Name**: Ensure `bucket_name` is globally unique.

4. **Initialize Terraform**
   Initialize the Terraform working directory:
   ```bash
   terraform init
   ```

5. **Plan the Infrastructure**
   Review the execution plan to confirm the resources to be created:
   ```bash
   terraform plan
   ```

6. **Apply the Configuration**
   Deploy the infrastructure:
   ```bash
   terraform apply
   ```
   - Type `yes` when prompted to confirm.

7. **Verify Outputs**
   Upon successful execution, Terraform will output important details such as:
   - VPC ID
   - Public Subnet IDs
   - Load Balancer DNS Name
   - S3 Bucket Name
   - Security Group ID

## Architecture Diagram

```
AWS Cloud
├── VPC (172.16.0.0/16)
│   ├── Public Subnet 1 (172.16.1.0/24)
│   │   └── Nginx Instance
│   ├── Public Subnet 2 (172.16.2.0/24)
│   │   └── Nginx Instance
│   └── Internet Gateway
│
├── Application Load Balancer
├── Auto Scaling Group (Min: 2, Max: 4)
└── S3 Bucket
```

## Key Components

1. **VPC**
   - CIDR Block: `172.16.0.0/16`
   - DNS Support: Enabled

2. **Subnets**
   - Two public subnets, each in a different availability zone.

3. **Internet Gateway**
   - Enables outbound internet access for resources within the VPC.

4. **Application Load Balancer (ALB)**
   - Distributes incoming traffic across Nginx instances.

5. **Auto Scaling Group (ASG)**
   - Maintains the desired capacity of two Nginx instances.

6. **Security Group**
   - Allows inbound HTTP traffic on port 80.

7. **Amazon S3 Bucket**
   - Storage bucket with versioning enabled.

## Clean Up

To destroy the infrastructure and avoid unnecessary charges:
```bash
terraform destroy
```
- Type `yes` when prompted to confirm.

## Important Notes

- Ensure your AWS credentials have sufficient permissions to create resources.
- Use a unique name for the S3 bucket to avoid naming conflicts.
- For production environments, consider adding SSL/TLS to the ALB for secure connections.

## Troubleshooting

- If Terraform commands fail, check the following:
  - AWS credentials are correctly exported.
  - The selected region supports all resources in the configuration.
  - The AMI ID is valid for the selected region.

## License
This project is licensed under the MIT License, which allows you to use, modify, and distribute the code for personal or commercial purposes as long as proper attribution is given. For more details, see the LICENSE file.


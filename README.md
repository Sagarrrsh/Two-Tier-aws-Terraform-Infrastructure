# Two-Tier-aws-Terraform-Infrastructure[terraform-aws-readme.md](https://github.com/user-attachments/files/22497807/terraform-aws-readme.md)
# Two-Tier AWS Terraform Infrastructure

A complete two-tier architecture on AWS using Terraform for Infrastructure as Code (IaC). This project provisions a scalable web application infrastructure with a presentation tier and data tier.

## Architecture Overview

This infrastructure includes:

- **Presentation Tier**: Web servers in public subnets
- **Data Tier**: Database servers in private subnets
- VPC with public and private subnets across multiple AZs
- Application Load Balancer for high availability
- Auto Scaling Groups for scalability
- RDS Database for data persistence
- Security Groups and NACLs for network security

## Prerequisites

Before deploying this infrastructure, ensure you have:

- [Terraform](https://www.terraform.io/downloads.html) (>= 1.0)
- [AWS CLI](https://aws.amazon.com/cli/) configured
- AWS account with appropriate permissions
- An AWS key pair for EC2 instances

## AWS Permissions Required

Your AWS user/role needs the following permissions:
- EC2 (instances, security groups, subnets, VPC)
- RDS (database instances, subnet groups)
- IAM (roles and policies)
- ELB (load balancers)
- Auto Scaling
- CloudWatch

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Sagarrrsh/Two-Tier-aws-Terraform-Infrastructure.git
cd Two-Tier-aws-Terraform-Infrastructure
```

### 2. Configure AWS Credentials

```bash
aws configure
```

Or set environment variables:
```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="us-east-1"
```

### 3. Initialize Terraform

```bash
terraform init
```

### 4. Review and Customize Variables

Copy and edit the variables file:
```bash
cp terraform.tfvars.example terraform.tfvars
```

Edit `terraform.tfvars` with your specific values:
```hcl
region = "us-east-1"
project_name = "two-tier-app"
vpc_cidr = "10.0.0.0/16"
key_pair_name = "your-key-pair"
db_username = "admin"
db_password = "your-secure-password"
```

### 5. Plan the Deployment

```bash
terraform plan
```

### 6. Deploy the Infrastructure

```bash
terraform apply
```

Type `yes` when prompted to confirm the deployment.

## Project Structure

```
Two-Tier-aws-Terraform-Infrastructure/
├── main.tf                 # Main Terraform configuration
├── variables.tf            # Input variables
├── outputs.tf             # Output values
├── terraform.tfvars       # Variable values (create this)
├── modules/               # Terraform modules
│   ├── vpc/
│   ├── security/
│   ├── compute/
│   └── database/
├── scripts/               # Bootstrap scripts
└── README.md
```

## Configuration Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `region` | AWS region | `us-east-1` | No |
| `project_name` | Project name for resource naming | `two-tier-app` | No |
| `vpc_cidr` | CIDR block for VPC | `10.0.0.0/16` | No |
| `key_pair_name` | EC2 Key Pair name | - | Yes |
| `db_username` | RDS master username | `admin` | No |
| `db_password` | RDS master password | - | Yes |
| `instance_type` | EC2 instance type | `t3.micro` | No |

## Outputs

After successful deployment, you'll get:

- Load Balancer DNS name
- VPC ID
- Public subnet IDs
- Private subnet IDs
- RDS endpoint
- Security Group IDs

## Usage

### Accessing the Application

Once deployed, access your application using the Load Balancer DNS name:
```
http://your-load-balancer-dns-name
```

### SSH Access to Web Servers

```bash
ssh -i your-key-pair.pem ec2-user@<instance-public-ip>
```

### Database Connection

Connect to the RDS instance from the web servers using the RDS endpoint provided in the outputs.

## Monitoring and Maintenance

### View Resources

```bash
# List all resources
terraform show

# Get specific outputs
terraform output
```

### Update Infrastructure

1. Modify the Terraform files
2. Plan the changes:
   ```bash
   terraform plan
   ```
3. Apply the changes:
   ```bash
   terraform apply
   ```

### Scaling

To scale the web tier:
1. Update the `desired_capacity` in the Auto Scaling Group configuration
2. Run `terraform apply`

## Cleanup

To destroy all resources:

```bash
terraform destroy
```

**⚠️ Warning**: This will permanently delete all resources created by this Terraform configuration.

## Security Considerations

- Web servers are in public subnets with restricted security groups
- Database servers are in private subnets (no direct internet access)
- Security groups follow the principle of least privilege
- Use strong passwords for RDS instances
- Regularly update AMIs and apply security patches

## Troubleshooting

### Common Issues

1. **Permission Denied**: Ensure your AWS credentials have sufficient permissions
2. **Key Pair Not Found**: Verify the key pair exists in your AWS region
3. **Resource Limits**: Check AWS service limits in your region
4. **State Lock**: If Terraform state is locked, wait or manually unlock

### Useful Commands

```bash
# Check Terraform version
terraform version

# Validate configuration
terraform validate

# Format code
terraform fmt

# Show current state
terraform show

# List resources in state
terraform state list
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

If you encounter any issues or have questions:

- Open an issue on GitHub
- Check AWS documentation for service-specific issues
- Review Terraform documentation for configuration questions

## Contact

Your Name - [@your_twitter](https://twitter.com/your_twitter) - your.email@example.com

Project Link: [https://github.com/Sagarrrsh/Two-Tier-aws-Terraform-Infrastructure](https://github.com/Sagarrrsh/Two-Tier-aws-Terraform-Infrastructure)

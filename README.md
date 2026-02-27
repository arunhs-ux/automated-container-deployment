# Automated Container Deployment in AWS

## Tools Used
- Terraform
- Ansible
- Docker
- GitHub Actions

## Deployment Steps

1. terraform init
2. terraform apply
3. Update ansible inventory with EC2 IP
4. ansible-playbook -i inventory playbook.yml
5. Push to GitHub to trigger CI/CD


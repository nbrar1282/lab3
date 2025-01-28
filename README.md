# lab3
# README.md

## Setup Instructions

### Prerequisites
Ensure you have the following installed:
- [Terraform](https://developer.hashicorp.com/terraform/downloads)
- [AWS CLI](https://aws.amazon.com/cli/)
- OpenSSH (for generating SSH keys and connecting to the instance)

---

## Task 1: Create an SSH Keypair

Generate an SSH keypair in your Linux environment:
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/aws_key -C "your-email@example.com"
```

The generated files:
- `~/.ssh/aws_key` (Private key - keep this secure)
- `~/.ssh/aws_key.pub` (Public key)

Update `cloud-config.yaml`, replacing `<public-key>` with the content of `~/.ssh/aws_key.pub`.

Set correct permissions for the private key:
```bash
chmod 600 ~/.ssh/aws_key
```

---

## Task 2: Terraform Configuration

### Initialize Terraform
```bash
terraform init
```

### Format Terraform Files
```bash
terraform fmt
```

### Plan the Deployment
```bash
terraform plan
```

### Apply the Configuration
```bash
terraform apply 
```

### Retrieve Instance Public IP
```bash
echo $(terraform output -json | jq -r '.instance_ip_addr.public_ip')
```

---

## Task 3: Connect to the Instance
Retrieve the Public IP or DNS and use SSH to connect:
```bash
ssh -i ~/.ssh/aws_key web@<public-ip>
```

If you get a **permissions error**, ensure the correct file permissions:
```bash
chmod 600 ~/.ssh/aws_key
```

Check if `nginx` is running:
```bash
curl http://<public-ip>
```

---

## Troubleshooting

### SSH Permission Denied Error
If you get an error like:
```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0777 for 'do-key' are too open.
```
Fix it by setting the correct permissions:
```bash
chmod 600 do-key
```

Then retry the SSH connection:
```bash
ssh -i do-key web@<public-ip>
```




---

# **AWS CLI, SDK, and CloudShell**

### **AWS CLI (Command Line Interface)**
- **Purpose**: Manage AWS services using command-line commands.
- **Credentials**: Access keys (**Access Key ID** and **Secret Access Key**) are needed to authenticate the CLI. Use `aws configure` to store these keys locally for CLI access.

---

### **AWS SDK (Software Development Kit)**
- **Purpose**: Enables developers to interact with AWS services programmatically using various languages like Python, JavaScript, and more.
- **Credentials**: Access keys are required for programmatic access. They can be provided through environment variables or within the application code.

---

### **AWS CloudShell**
- **Purpose**: A browser-based shell with AWS CLI pre-installed for quick management of AWS resources.
- **Credentials**: No access keys are required. It uses session-based credentials from your logged-in AWS Console session.

# **Configuring Access to AWS CLI**

### **1. Access Keys**

- **What Are Access Keys?**: Consist of an **Access Key ID** and a **Secret Access Key**, these are required for programmatic access to AWS services.
- **How to Create Access Keys**:
  1. In the AWS Management Console, navigate to **IAM** > **Users**.
  2. Select a user and go to the **Security Credentials** tab.
  3. Create and download **Access Key ID** and **Secret Access Key**.
- **Configure CLI**:
  - Run `aws configure` and provide the **Access Key ID**, **Secret Access Key**, default region, and output format.
  - Store them securely and avoid hardcoding them in applications.

---

### **2. SSH Access for EC2**

- **What is SSH?**: Secure Shell (SSH) is used for securely accessing EC2 instances via terminal.
- **Create SSH Key Pair**:
  1. In the AWS Console, go to **EC2** > **Key Pairs**.
  2. Create a new key pair and download the private key.
- **Use SSH to Access EC2**:
  - After launching an EC2 instance, use `ssh -i "your-key.pem" ec2-user@<EC2-instance-public-IP>` to access it.

---

### **Best Practices**
- Rotate access keys regularly and delete unused ones.
- Use IAM roles wherever possible instead of long-term access keys.
- Store private SSH keys securely and avoid sharing them.

# **AWS CLI & EC2 Virtual Machine**

---

## **1. Introduction**

AWS CLI (Command Line Interface) allows you to manage AWS resources programmatically. You can:

* Launch and manage **EC2 instances (virtual machines)**
* Automate tasks using scripts
* Integrate AWS operations into DevOps pipelines
* Work across **multiple accounts, regions, and environments**

**EC2 (Elastic Compute Cloud)** enables scalable virtual servers with customizable CPU, memory, storage, and networking.

---

## **2. Prerequisites**

1. **AWS Account** – Sign up at [AWS](https://aws.amazon.com/).
2. **Install AWS CLI** – [Official guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
3. **Install jq** – Parse CLI JSON output:

   ```bash
   sudo apt install jq      # Ubuntu
   brew install jq          # MacOS
   ```
4. **Install optional tools for remote access**

   * **MobaXterm (Windows)**: [Download](https://www.mobaxterm.mobatek.net/download.html)
   * **NoMachine**: [Download](https://www.nomachine.com/download)
5. **SSH Key Pair** – Required to access EC2 instances securely.

---

## **3. Configure AWS CLI**

Authenticate and configure AWS CLI to use credentials.

```bash
# Default profile
aws configure
# Enter:
# AWS Access Key ID: <YourAccessKey>
# AWS Secret Access Key: <YourSecretKey>
# Default region: <region-name>
# Output format: json | yaml | table | text
```

**Optional: Multiple Profiles**

```bash
aws configure --profile dev-profile
aws s3 ls --profile dev-profile
```

**Verify Configuration**

```bash
aws sts get-caller-identity  # Returns account & ARN
aws s3 ls                     # List S3 buckets
```

---

## **4. AWS CLI Pro-Tips**

1. **Command Completion**: Tab for auto-completion

   * [Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-completion.html)

2. **Help Command**: Access detailed CLI docs

```bash
aws help
aws ec2 help
aws s3 help
```

3. **jq for JSON parsing**

```bash
aws ec2 describe-instances | jq -r '.Reservations[].Instances[].InstanceId'
```

4. **Default Output Formats**: json, yaml, table, text. Use table for readable CLI display.

5. **Use Environment Variables** (optional for temporary credentials)

```bash
export AWS_ACCESS_KEY_ID=<access-key>
export AWS_SECRET_ACCESS_KEY=<secret-key>
export AWS_DEFAULT_REGION=us-east-1
```

---

## **5. EC2 Virtual Machine Management**

### **5.1 Launch EC2 Instance**

```bash
aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --count 1 \
  --instance-type t2.micro \
  --key-name MyKeyPair \
  --security-group-ids sg-0123456789abcdef0 \
  --subnet-id subnet-0123456789abcdef0 \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=MyServer}]'
```

**Explanation**:

* `--image-id`: AMI ID
* `--instance-type`: VM hardware
* `--key-name`: SSH key for secure login
* `--security-group-ids`: Firewall settings
* `--subnet-id`: Networking configuration
* `--tag-specifications`: Name your instance

---

### **5.2 List Instances**

```bash
aws ec2 describe-instances | jq -r '.Reservations[].Instances[] | .InstanceId + " " + .InstanceType + " " + (.Tags[] | select(.Key=="Name").Value)'
```

---

### **5.3 Start / Stop / Terminate**

```bash
aws ec2 start-instances --instance-ids i-0123456789abcdef0
aws ec2 stop-instances --instance-ids i-0123456789abcdef0
aws ec2 terminate-instances --instance-ids i-0123456789abcdef0
```

---

### **5.4 Security Groups**

**List Security Groups**

```bash
aws ec2 describe-security-groups | jq -r '.SecurityGroups[] | .GroupId + " " + .GroupName'
```

**Add Rule (SSH, HTTP, HTTPS)**

```bash
aws ec2 authorize-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 22 --cidr 0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 80 --cidr 0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 443 --cidr 0.0.0.0/0
```

**Remove Rule**

```bash
aws ec2 revoke-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 22 --cidr 0.0.0.0/0
```

**Edit Rules**

```bash
aws ec2 update-security-group-rule-descriptions-ingress --group-id sg-0123456789abcdef0 --ip-permissions 'ToPort=443,IpProtocol=tcp,IpRanges=[{CidrIp=203.0.113.1/32,Description="Office"}]'
```

---

### **5.5 Connect via SSH**

**Prepare Key**

```bash
chmod 400 MyKeyPair.pem
```

**SSH Command**

```bash
ssh -i MyKeyPair.pem ec2-user@<Public-IP-of-instance>
```

**MobaXterm**

* Open MobaXterm → Sessions → SSH
* Host: `<Public-IP>`
* Specify private key: `MyKeyPair.pem`
* Connect

---

### **5.6 Elastic IPs (Static Public IP)**

```bash
# Allocate Elastic IP
aws ec2 allocate-address --domain vpc

# Associate Elastic IP with instance
aws ec2 associate-address --instance-id i-0123456789abcdef0 --allocation-id eipalloc-12345678
```

---

### **5.7 Snapshots and AMIs**

**Create Snapshot of Volume**

```bash
aws ec2 create-snapshot --volume-id vol-0123456789abcdef0 --description "Backup snapshot"
```

**Create Custom AMI**

```bash
aws ec2 create-image --instance-id i-0123456789abcdef0 --name "MyServer-AMI" --no-reboot
```

---

### **5.8 Monitoring & Logs**

**Check Instance Status**

```bash
aws ec2 describe-instance-status --instance-ids i-0123456789abcdef0
```

**Enable CloudWatch Monitoring**

```bash
aws ec2 monitor-instances --instance-ids i-0123456789abcdef0
aws ec2 describe-instances --instance-ids i-0123456789abcdef0 | jq '.Reservations[].Instances[] | {InstanceId, State, Monitoring}'
```

---

## **6. AWS CLI for Common Services**

### **6.1 S3**

```bash
# List buckets
aws s3 ls

# Upload file
aws s3 cp localfile.txt s3://mybucket/

# Download file
aws s3 cp s3://mybucket/remote.txt ./local.txt

# Sync folder
aws s3 sync ./local_folder s3://mybucket/
```

### **6.2 IAM**

```bash
# List users
aws iam list-users | jq -r '.Users[].UserName'

# Create user
aws iam create-user --user-name newuser

# Attach policy
aws iam attach-user-policy --user-name newuser --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

### **6.3 CloudWatch**

```bash
# List alarms
aws cloudwatch describe-alarms | jq -r '.MetricAlarms[] | .AlarmName + " " + .StateValue'

# Create alarm
aws cloudwatch put-metric-alarm --alarm-name CPUAlarm --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 80 --comparison-operator GreaterThanThreshold --evaluation-periods 2 --alarm-actions <SNS-ARN> --dimensions Name=InstanceId,Value=i-0123456789abcdef0
```

### **6.4 DynamoDB**

```bash
# List tables
aws dynamodb list-tables | jq -r '.TableNames[]'

# Scan table
aws dynamodb scan --table-name MyTable

# Get item
aws dynamodb get-item --table-name MyTable --key '{"email": {"S": "user@example.com"}}'
```

---

## **7. Automation & Scripting**

* **Bash Script Example: Automated EC2 Launch**

```bash
#!/bin/bash
INSTANCE_ID=$(aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --instance-type t2.micro \
  --key-name MyKeyPair \
  --security-group-ids sg-0123456789abcdef0 \
  --subnet-id subnet-0123456789abcdef0 \
  --query 'Instances[0].InstanceId' --output text)
echo "Launched EC2 instance: $INSTANCE_ID"
```

* **Scheduled Backups using cron**

```bash
0 2 * * * /usr/bin/aws ec2 create-snapshot --volume-id vol-0123456789abcdef0 --description "Daily backup"
```

---

## **8. Security Best Practices**

* Always use **IAM roles** for EC2 instances instead of embedding access keys.
* Avoid using `0.0.0.0/0` for SSH in production. Restrict IP ranges.
* Enable **CloudTrail** to track all AWS CLI activities.
* Rotate access keys regularly.

---

## **9. Troubleshooting Tips**

* **Access Denied** → Check IAM permissions
* **SSH Timeout** → Check Security Groups & Network ACLs
* **CLI Not Found** → Check AWS CLI installation and PATH variable
* **jq Errors** → Validate JSON output

---

## **10. References**

* AWS CLI Docs: [https://docs.aws.amazon.com/cli/](https://docs.aws.amazon.com/cli/)
* EC2 CLI Reference: [https://docs.aws.amazon.com/cli/latest/reference/ec2/index.html](https://docs.aws.amazon.com/cli/latest/reference/ec2/index.html)
* jq GitHub: [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)

# ░░░░░░░░░░░ **Boto3** ░░░░░░░░░░░░░░░░░░░


## **1️⃣ What is Boto3?**

* **Boto3** is the official **AWS SDK for Python**.
* It allows you to **create, configure, and manage AWS services** (like EC2, S3, DynamoDB) directly from Python scripts.
* Perfect for **automation, DevOps tasks, or building AWS-integrated applications**.

---

## **2️⃣ Installing Boto3**

```bash
pip install boto3
```

> Make sure Python is installed and `pip` is available.

---

## **3️⃣ AWS Authentication with Boto3**

Boto3 looks for credentials in the following order:

1. **Environment variables**:

```bash
export AWS_ACCESS_KEY_ID=your_access_key
export AWS_SECRET_ACCESS_KEY=your_secret_key
export AWS_DEFAULT_REGION=us-east-1
```

2. **AWS CLI credentials file** (from `aws configure`):

```bash
~/.aws/credentials
```

3. **Explicitly in code**:

```python
import boto3

session = boto3.Session(
    aws_access_key_id='YOUR_KEY',
    aws_secret_access_key='YOUR_SECRET',
    region_name='us-east-1'
)
```

---

## **4️⃣ Example: Launch EC2 Instance with Boto3**

```python
import boto3

# Create EC2 client
ec2 = boto3.client('ec2', region_name='us-east-1')

# Launch instance
response = ec2.run_instances(
    ImageId='ami-0abcdef1234567890',  # Ubuntu AMI
    MinCount=1,
    MaxCount=1,
    InstanceType='t2.micro',
    KeyName='MyKeyPair',
    SecurityGroupIds=['sg-0123456789abcdef0'],
    SubnetId='subnet-0abc12345def67890',
    TagSpecifications=[
        {
            'ResourceType': 'instance',
            'Tags': [{'Key': 'Name', 'Value': 'MyPythonVM'}]
        }
    ]
)

print("Launched EC2 Instance:", response['Instances'][0]['InstanceId'])
```

---

## **5️⃣ Example: List S3 Buckets**

```python
import boto3

s3 = boto3.client('s3')

response = s3.list_buckets()
for bucket in response['Buckets']:
    print(bucket['Name'])
```

---

## **6️⃣ Example: Upload a File to S3**

```python
s3 = boto3.client('s3')

s3.upload_file('local_file.txt', 'my-bucket', 'remote_file.txt')
print("File uploaded successfully")
```

---

## **7️⃣ Example: Automate EC2 Termination**

```python
ec2 = boto3.client('ec2')

# Terminate instance
ec2.terminate_instances(InstanceIds=['i-0abcdef1234567890'])
print("Instance terminated")
```

---

## **Pro Tips**

* Use **boto3 resource vs client**:

  * `client` → low-level, closer to API calls
  * `resource` → high-level, object-oriented abstraction
* Always handle exceptions with `try/except`.
* Great for **DevOps automation, scheduled scripts, or AWS-integrated applications**.



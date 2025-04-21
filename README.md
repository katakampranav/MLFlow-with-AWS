# MLFLOW On AWS

## MLflow on AWS Setup:

1. Login to AWS console.  
2. Create an IAM user with **AdministratorAccess**.  
3. Export the credentials in your AWS CLI by running `aws configure`.  
4. Create an **S3 bucket**.  
5. Create an **EC2 machine (Ubuntu)** & add a **Security Group rule to allow port 5000** (Custom TCP -> 5000 -> Anywhere).

---

### On the EC2 instance, run the following:

```bash
sudo apt update

sudo apt install python3-pip -y

sudo apt install pipenv -y

sudo apt install virtualenv -y

mkdir mlflow

cd mlflow

# Download or create requirements.txt if needed, OR install directly

pipenv install mlflow

pipenv install awscli

pipenv install boto3

pipenv shell
```

---

### Then set AWS credentials:

```bash
aws configure
```

> Here you will be prompted for your **Access Key ID**, **Secret Access Key**, **Region**, and **Output format**.  
> These come from the IAM user you created earlier.

---

### Finally, run the MLflow server:

```bash
mlflow server -h 0.0.0.0 -p 5000 --default-artifact-root s3://your_s3_bucket_name
```

> Make sure to **replace** `your_s3_bucket_name` with your actual S3 bucket name.

> You can access the MLflow UI by opening **Public IPv4 DNS** of your EC2 instance on **port 5000** (e.g., `http://ec2-xx-xxx-xxx-xx.compute-1.amazonaws.com:5000`)

---

### Set tracking URI in your local terminal or Python code:

**Option 1 – Terminal:**
```bash
export MLFLOW_TRACKING_URI=http://<your-ec2-public-dns>:5000/
```

**Option 2 – Python code:**
```python
import os
os.environ['MLFLOW_TRACKING_URI'] = "http://<your-ec2-public-dns>:5000/"
```
### Flow
![Image](https://github.com/user-attachments/assets/d7c94683-e63c-46ea-b7fd-0dea8db57a5e)
---

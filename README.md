# aws-azure-multicloud-lambda

# 🌐 AWS-Azure MultiCloud Deployment Pipeline

This project demonstrates a fully functional multi-cloud file transfer pipeline using **AWS S3**, **Lambda**, and **Microsoft Azure Blob Storage**. Upon upload of a file to an S3 bucket, an AWS Lambda function automatically transfers the file to a designated Azure container — enabling real-time data sharing across cloud platforms.

## 🔧 Technologies Used
- **AWS S3** – File upload and event triggering
- **AWS Lambda** – File transfer logic via Python 3.9
- **Azure Blob Storage** – Destination container for cross-cloud delivery
- **IAM Policies and Roles** – Secure access management
- **Lambda Layers** – Custom dependencies with Python support
- **CloudWatch Logs** – Execution logging and observability

## 📁 Architecture Overview
```
S3 Bucket (pgpcc02051320)
   └── triggers Lambda Function (AWSandAzureMultiCloud)
         └── uses Lambda Layer (S3azurelayer.zip)
               └── pushes file to Azure Blob Container ("name")
```

## 🚀 Deployment Steps

### AWS Setup
1. **Create S3 Bucket:** `pgpcc02051320`
2. **Define IAM Policy & Role:** `MultiCloudPolicyAWSandAzure` and `MultiCloudAWSandAzure`
3. **Create Lambda Layer:** Upload `S3azurelayer.zip`
4. **Deploy Lambda Function:** Python 3.9 runtime with 2048MB storage and 50s timeout
5. **Configure Environment Variables:**
   - `AZURE_CONTAINER_NAME`
   - `AZURE_STORAGE_CONNECTION_STRING`
6. **Attach S3 Trigger:** Event type `Put` with recursion warning acknowledgement

### Azure Setup
1. **Create Resource Group:** `AWSandAzureMultiCloud`
2. **Deploy Storage Account:** `awsandazuremulticloud` with LRS redundancy
3. **Create Blob Container:** Name specified in environment variable
4. **Copy Connection String:** Used by Lambda to authenticate with Azure

## 📄 Sample Workflow
1. User uploads `wine.csv` to AWS S3 bucket.
2. Lambda function detects the event and triggers file transfer logic.
3. File appears in Azure Blob container titled `name`.

## 🔒 Security & Optimization
- IAM permissions scoped to required services (S3, CloudWatch Logs).
- Sensitive connection strings injected securely via environment variables.
- Warning configured for recursive invocation risks.

## 📌 Status
✅ **Deployment successful** — tested with `wine.csv` file upload

## 🧠 Lessons Learned
- Lambda execution roles require precise policy attachment for cross-service interaction.
- Azure storage connection string injection must be correctly formatted to ensure authentication.
- S3 event filtering reduces unnecessary invocations and associated costs.

## 📚 References
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Azure Blob Storage Overview](https://learn.microsoft.com/en-us/azure/storage/blobs/)


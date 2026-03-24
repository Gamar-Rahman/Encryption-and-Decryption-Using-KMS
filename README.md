# Encryption-and-Decryption-Using-KMS
 Encryption & Decryption Using AWS KMS (EC2 + IAM)

### Overview
This project demonstrates how to securely perform encryption and decryption using AWS KMS, integrated with:
Amazon EC2 for compute
IAM for access control
KMS for key management

### Key Concepts
🔹 What is Amazon EC2?

EC2 provides scalable compute instances where applications and scripts run securely.

🔹 What is IAM?

IAM controls who can access and use AWS resources, including encryption keys.

🔹 What is AWS KMS?

AWS KMS is a managed service for creating and managing encryption keys using Hardware Security Modules (HSMs).

### Problem Statement

Sensitive data is often:

Stored without encryption
Accessed without strict controls
Exposed due to poor key management

### The challenge:
How do we securely encrypt data and control who can decrypt it?

### Solution

We implemented:

Customer-managed KMS key
IAM users & groups with controlled permissions
EC2 instance to perform encryption/decryption
Secure key usage policies

### Implementation Steps

🔹 Step 1: Create IAM Group & Users
Define KMS permissions
Attach least privilege policies

🔹 Step 2: Create KMS Key
Customer-managed key (CMK)
Configure key policy

🔹 Step 3: Launch EC2 Instance
Configure IAM role / access
SSH into instance

🔹 Step 4: Encrypt Data
aws kms encrypt \
  --key-id <KMS_KEY_ID> \
  --plaintext "Sensitive Data" \
  --output text \
  --query CiphertextBlob

🔹 Step 5: Decrypt Data

 aws kms decrypt \
  --ciphertext-blob fileb://encrypted.txt \
  --output text \
  --query Plaintext | base64 --decode

  ### Testing

  | Test Case                       | Result    |
| ------------------------------- | --------- |
| Encryption using KMS            | Success ✅ |
| Decryption with authorized user | Success ✅ |
| Unauthorized access             | Blocked ❌ |

### Security Insight
Encryption is only as strong as your key management.
KMS ensures:
Secure key storage
Controlled access
Audit-ready operations

### Future Improvements
Integrate CloudTrail for key usage monitoring
Use envelope encryption
Apply KMS with S3/EBS
Add automatic key rotation

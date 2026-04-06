# Deployment Steps – Cross Account Access

This guide shows how to enable cross-account access to an S3 bucket using an IAM role.

---

## 1. Dev Account – Create IAM User
1. IAM → Create user → Name: `Alice`  
2. Provide AWS Management Console access  
3. Set custom password and uncheck “User must create a new password at next sign-in”  
4. Copy credentials:
   - Console sign-in URL: `https://accountid.signin.aws.amazon.com/console`  
   - User: `Alice`  
   - Password: `your-custom-password`
---
## 2. Prod Account – Create S3 Bucket and IAM Role
1. S3 → Create bucket → Name: `bucket-14-11-25`  
2. Upload an object to the bucket  
3. IAM → Roles → Create role  
   - Trusted entity: AWS Account → Another AWS Account → Dev Account ID  
   - Permissions: AmazonS3FullAccess  
   - Role name: `crossaccountaccess`
---
## 3. Dev Account – Attach Inline Policy to Alice
JSON Example:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "sts:AssumeRole",
      "Resource": "arn:aws:iam::PROD_ACCOUNT_ID:role/crossaccountaccess"
    }
  ]
}
```
Alternatively, create the policy using the visual editor:
- Service: `STS`
- Actions: All actions (`sts:*`)
- Resources: All
- Policy name: `stspolicy`

---
## 4. Switch Role and Access Bucket
1. Open a browser in Incognito mode
2. Log in as `Alice` using the Dev account console URL
3. Click your account name (top right) → **Switch Role**
4. Enter:
   - Account: `PROD_ACCOUNT_ID`
   - Role: `crossaccountaccess`
   - Display name: `crossaccountaccess@123`
5. Click **Switch Role**
6. Open S3 → navigate to `bucket-14-11-25`
7. Confirm you can view and access the objects

---
> ✅ Deployment complete. Alice can now securely access the S3 bucket in the Prod account by assuming the IAM role.

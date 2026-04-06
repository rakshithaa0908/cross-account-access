# Cross Account S3 Access Using IAM Roles

This project demonstrates how to securely grant users or services from one AWS account access to an S3 bucket in another account using IAM roles.

---

## Concepts

### Authentication
Confirming the identity of a user, typically via username and password.

### Authorization
Determines what actions an authenticated user or service is allowed to perform on AWS resources.

### IAM User vs IAM Role

| IAM User | IAM Role |
|----------|----------|
| Permanent identity | Temporary identity (e.g., 1 hour in Free Tier) |
| Long-term credentials | Temporary credentials |
| Direct AWS Console access | Assumed by users or services |

### Policies

| Feature | Customer Managed Policy | Inline Policy |
|---------|-----------------------|---------------|
| Reusability | Yes, can attach to multiple entities | No, embedded in a single entity |
| Management | Standalone with versioning | Managed within entity, no versioning |
| Lifecycle | Exists until deleted | Deleted with associated entity |

Cross-account access allows users or services from one account to securely access resources in another by assuming a role.

### Technologies Used
- AWS IAM (Identity and Access Management)
- AWS S3
- IAM Roles and Policies
- Cross-Account Role Assumption
- AWS Management Console
---

## Prerequisites
- Two AWS accounts (Account A and Account B)
- IAM user with appropriate permissions in Account A
- Basic knowledge of AWS IAM and S3
---

## Deployment Steps

See full deployment instructions [here](docs/deployment-steps.md).

---

## Project Structure
```
cross-account-access/
│
├── docs/
│   ├── deployment-steps.md
│   └── screenshots/
│       ├── cross_account_access.png
│       └── cross_account_architecture.png
├── README.md
└── LICENSE
```
## Architecture Diagram
![Architecture](docs/screenshots/cross_account_architecture.png)

## Screenshots

**Cross Account Access**
![Cross Account Access](docs/screenshots/cross_account_access.png)

---
## About This Project
Built to demonstrate secure cross-account access in AWS using IAM roles. Instead of sharing long-term credentials, Account A users assume a role in Account B to temporarily access S3 resources — following AWS security best practices.

---

## Limitations
- Temporary credentials expire after a set duration (1 hour on Free Tier)
- Requires trust policy and permission policy to be configured correctly in both accounts
- Does not cover cross-account access via S3 bucket policies
- Intended for learning and demonstration purposes only

---

## License

MIT License. See `LICENSE` file for details.




# IAM Assignment Submission

**Student Name:**  Sylvia
**Date:**  26.11.25
**Time Spent:** 3+

---

## Task 1: IAM Groups

### Screenshots
- [ ] Groups list
- [ ] DatabaseAdmins permissions
- [ ] JuniorDevelopers permissions
<img width="1910" height="832" alt="DatabaseAdmins   JuniorDevelopers-Task 1" src="https://github.com/user-attachments/assets/112dfc6f-227c-406e-b5bc-3e98f19c498e" />
### Notes


---

## Task 2: IAM Users

### Screenshots
- [ ] Users list
- [ ] db-admin group membership
- [ ] dev-junior group membership
<img width="1911" height="836" alt="db-admin-Sylvia   dev-junior-Sylvia-Task 2" src="https://github.com/user-attachments/assets/054b2432-fba0-4bda-a5df-d2a9017e50ae" />
<img width="1901" height="837" alt="db-admin-Sylvia-membership-Task2" src="https://github.com/user-attachments/assets/1ab1e069-9e9e-4d9e-acc8-20fe83ff46a2" />
<img width="1911" height="838" alt="dev-junior-Sylvia-membership-Task2" src="https://github.com/user-attachments/assets/c3cab441-4dd3-4eb1-aba9-79bdf4bdbe38" />

### Notes


---

## Task 3: Custom Policy

### Screenshots
- [ ] Policy in IAM console
- [ ] Policy JSON view
<img width="1883" height="832" alt="Custom Policy-Task 3" src="https://github.com/user-attachments/assets/432f3923-4477-4813-bf71-2e1f379731e2" />

### Your Policy JSON
```json
{
  "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowS3ReadForWebappBuckets",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectVersion",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::webapp-*",
                "arn:aws:s3:::webapp-*/*"
            ]
        },
        {
            "Sid": "AllowDynamoDBWriteForWebappTables",
            "Effect": "Allow",
            "Action": [
                "dynamodb:PutItem",
                "dynamodb:BatchWriteItem",
                "dynamodb:UpdateItem"
            ],
            "Resource": [
                "arn:aws:dynamodb:*:*:table/webapp-*"
            ]
        },
        {
            "Sid": "DenyDeleteActionsForS3AndDynamoDB",
            "Effect": "Deny",
            "Action": [
                "s3:DeleteObject",
                "s3:DeleteObjectVersion",
                "s3:DeleteBucket",
                "dynamodb:DeleteItem",
                "dynamodb:DeleteTable"
            ],
            "Resource": [
                "arn:aws:s3:::*",
                "arn:aws:s3:::*/*",
                "arn:aws:dynamodb:*:*:table/*"
            ]
        }
    ]
}
```

### Explanation
Why did you choose these specific actions and resources?
- s3:GetObject lets the server read/download objects (files) like static assets or config files.
- s3:ListBucket is optionally required if your code lists objects in the bucket (e.g., enumerate files). It is applied at the bucket ARN (no /*).
- dynamodb:BatchWriteItem — useful if the app uses batch writes.
---

## Task 4: IAM Role

### Screenshots
- [ ] Role summary
- [ ] Trust relationships
- [ ] Attached policies
<img width="1895" height="828" alt="Attachment of EC2 instance-Task4" src="https://github.com/user-attachments/assets/4d54c65d-1c62-48cb-a4c6-184f75f7c8f4" />
<img width="1897" height="771" alt="WebServerRole-Sylvia-Custom Policy-Task4" src="https://github.com/user-attachments/assets/bb58e5a5-834a-4d0b-bc31-09b5a8399daa" />
<img width="1897" height="840" alt="WebServerRole-Sylvia-Task4" src="https://github.com/user-attachments/assets/50d3ce9c-4f53-402a-b601-9fc788338ec7" />
<img width="1893" height="832" alt="WebServerRole-Sylvia-Trust Relationship-Task4" src="https://github.com/user-attachments/assets/2a60b842-7eec-4040-b613-ecc0c4e1c28e" />

### Notes
---

## Task 5: User Permission Tests

### db-admin User
- [ ] Successful RDS access
- [ ] Denied access to another service
<img width="1908" height="831" alt="Other Services-Failure 1-Task5" src="https://github.com/user-attachments/assets/fdfa114e-24e5-4c93-9d24-543b983dbdde" />
<img width="1907" height="837" alt="Other Services-Failure-Task5" src="https://github.com/user-attachments/assets/25e7255c-47f9-4c44-b04a-8a562399567e" />

### dev-junior User
- [ ] Successful CloudWatch access
- [ ] Denied access to another service
<img width="1903" height="885" alt="Failure-Other Services (CloudWatch)-Task5" src="https://github.com/user-attachments/assets/b8e43843-ef3a-4f74-9ce7-c0c21fd2f478" />

### Observations
---
## Task 6: EC2 Role Tests

### Screenshots
- [ ] Role attached to EC2
- [ ] Successful operations (with correct prefix)
- [ ] Failed operations (wrong prefix or delete)
<img width="1915" height="771" alt="Correct Prefix-Task6" src="https://github.com/user-attachments/assets/01ad1bc6-043f-485f-9d48-496dcf1f4480" />
<img width="1908" height="100" alt="Wrongprefix-Task6" src="https://github.com/user-attachments/assets/2e0d46ea-1063-4b13-a4f4-29d553ce6e14" />
<img width="923" height="500" alt="Wrong prefixor no delete permission-Task6" src="https://github.com/user-attachments/assets/53cc2881-d769-412c-9b64-8d90ec832803" />

### Explanation
Why did each operation succeed or fail?
- Create S3 bucket with correct prefix succeeded because IAM policy allows this prefix.   
- Create S3 bucket with wrong prefix  failed because IAM policy blocks other prefixes.
- Deleting S3 bucket failed because IAM policy denies deleting.
- Create DynamoDB table with correct prefix succeeded because IAM policy allows this prefix.
- Create DynamoDB table with wrong prefix failed because IAM policy denies other prefixes.
- Delete DynamoDB table failed because IAM policy denies delete.
---

## Task 7: Security Questions

**Q1: Why use groups vs direct policy attachment?**

**Answer:**
Groups make permissions easier to manage and scale.

**Q2: Why restrict to webapp-* prefix?**

**Answer:**
This is because it enforces resource isolation.

**Q3: Can WebServerRole be used by Lambda?**

**Answer:**
It might work if the role has the correct trust policy.

**Q4: Is DatabaseAdmin "FullAccess" least privilege?**

**Answer:**
No, it violates the Principle of Least Privilege, which says users should have only the permissions they need.

**Q5: Difference between bucket ARN and bucket/* ARN?**

**Answer:**
arn:aws:s3:::my-bucket refers to the bucket itself, e.g., for creating or deleting the bucket.

arn:aws:s3:::my-bucket/* refers to all objects inside the bucket, e.g., uploading, reading, or deleting files.

**Q6: How do credentials auto-rotate?**

**Answer:**
EC2 instances that use an IAM role get temporary credentials from the Instance Metadata Service (IMDS).
These credentials automatically expire every few hours. Before they expire, IMDS provides new, fresh credentials to the instance.

**Q7: EC2 compromised - what to do? (A/B/C/D)**

**Answer:**
B) Revoke the IAM role’s active sessions
**Reasoning:**
Lets say for example, if an attacker has taken control of your EC2 instance, they are using the IAM role attached to it and so the fastest and most effective way to stop them is to revoke all active role sessions.
---

## Task 8: BONUS - MFA

### Screenshots
- [ ] MFA on db-admin
- [ ] MFA on dev-junior
- [ ] MFA login prompt
<img width="1908" height="881" alt="MFA enabled-Task8" src="https://github.com/user-attachments/assets/ea05eab8-4d65-4212-ab9f-a5c9a1525a52" />
<img width="1906" height="1002" alt="MFA login prompt-Task8" src="https://github.com/user-attachments/assets/aaa5b17f-4fec-4f09-83bb-a6e058d432e2" />

### Notes
---

## Task 9: Cleanup

### Screenshots
- [ ] Users deleted
- [ ] Groups deleted
- [ ] Role deleted
- [ ] Policy deleted
- [ ] EC2 terminated
<img width="1918" height="882" alt="DatabaseAdmins deleted-Task9" src="https://github.com/user-attachments/assets/1d05480e-d7c9-4162-a77d-5956d6724960" />
<img width="1915" height="882" alt="dev-junior-Sylvia deleted- Task9" src="https://github.com/user-attachments/assets/fdb42950-9876-4c4d-bc8a-4611aba23786" />
<img width="1912" height="882" alt="DynamoDB table 1 deleted-Task9" src="https://github.com/user-attachments/assets/16716c2a-bde1-4537-bf95-b05a95a1f4aa" />
<img width="1908" height="883" alt="DynamoDB table 2 deleted-Task9" src="https://github.com/user-attachments/assets/5e4c362a-b545-4a5a-b55e-1719dff4e268" />
<img width="1912" height="878" alt="juniorDevelopers deleted-Task9" src="https://github.com/user-attachments/assets/872a7ec6-de84-4c0f-af50-575e0b69441d" />
<img width="1906" height="831" alt="JuniorDevelopers-policies-Task9" src="https://github.com/user-attachments/assets/4404e3b2-199f-499e-8aa6-82dc0785dc0e" />
<img width="1905" height="886" alt="user db-admin-Sylvia deleted-Task9" src="https://github.com/user-attachments/assets/dd77aa1b-feec-4387-a573-619079f7a531" />
<img width="1916" height="881" alt="webapp-bucket-sylvia-123 deleted-Task9" src="https://github.com/user-attachments/assets/8dcc273c-a56a-4d3b-87ea-06411b38f450" />
<img width="1897" height="882" alt="WebServerPolicy deleted-Task9" src="https://github.com/user-attachments/assets/44c26562-8f2a-4090-a62a-dc27e1e17506" />
<img width="1916" height="883" alt="WebServerRole-Sylvia deleted-Task9" src="https://github.com/user-attachments/assets/3e117c0b-bd60-491c-a5cd-861951d61985" />
<img width="1893" height="822" alt="wrongprefix-bucket-sylvia-123 deleted-Task9" src="https://github.com/user-attachments/assets/bf88bfca-b67d-46fb-a9c1-aec75c238b4a" />

---

## Reflection

**Most challenging part:**
The most challenging part was managing IAM permissions and understanding why certain actions were denied. Troubleshooting AccessDenied errors required carefully checking trust policies, resource ARNs, and prefix restrictions. It was also time consuming for me to understand how AWS CLI users, IAM users, and EC2 roles interact differently.
**What I learned:**
The assignment helped me understand practical, real-world cloud security architecture.
**What I'd do differently in production:**
In a real production environment, I would enforce stricter least-privilege principles, avoid using broad policies like FullAccess, and rely heavily on IAM roles instead of long-term access keys. I would also implement MFA for all users.
---

**Submission Checklist:**
- [ ] All screenshots included
- [ ] All questions answered
- [ ] Policy JSON included
- [ ] No credentials visible
- [ ] Resources cleaned up

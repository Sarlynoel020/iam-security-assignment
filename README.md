# IAM Security Assignment

 
Deadline: No later than 10:00 aM ET on 22 October 2025


## 🎯 Objective

Demonstrate your understanding of IAM by building a secure setup for a 3-tier web application.

**You will create:**
- IAM Groups for team organization
- IAM Users for human access
- IAM Roles for EC2 instances
- Custom Policies with least-privilege access

---

## 📋 Requirements

### Task 1: Create IAM 

Create **two groups** with appropriate policies:

**Group 1: DatabaseAdmins**
- These users need to manage RDS databases
- Find and attach the appropriate AWS managed policy for RDS full access

**Group 2: JuniorDevelopers**  
- These users should only be able to VIEW application logs
- Find and attach the appropriate AWS managed policy for CloudWatch Logs read-only access

**What to submit:**
- Screenshots of both groups
- Screenshots showing the policies attached to each group

---

### Task 2: Create IAM Users 

Create **two test users**:

**User 1:** Database administrator
- Naming convention: `db-admin-[yourname]`
- Should be able to log into AWS Console
- Add to the DatabaseAdmins group

**User 2:** Junior developer
- Naming convention: `dev-junior-[yourname]`
- Should be able to log into AWS Console
- Add to the JuniorDevelopers group

**What to submit:**
- Screenshots showing both users created
- Screenshots showing each user's group membership

---

### Task 3: Create Custom Policy 

**Scenario:** Your web servers need to:
- Read files from S3 buckets (but only buckets that start with `webapp-`)
- Write data to DynamoDB tables (but only tables that start with `webapp-`)
- Should NOT be able to delete anything
- Should NOT access resources that don't have the `webapp-` prefix

**Your task:**
- Create a custom IAM policy named `WebServerPolicy-[yourname]`
- Write the policy JSON that implements the requirements above
- The policy should follow the Principle of Least Privilege

**Hints:**
- Review the policy structure we learned in class
- You'll need to use S3 and DynamoDB actions
- Think about how to restrict using the Resource field
- Use wildcards (`*`) appropriately for the prefix matching

**What to submit:**
- Screenshot of your custom policy in IAM
- The complete policy JSON (copy/paste into your submission)
- Brief explanation of why you chose those specific actions and resources

---

### Task 4: Create IAM Role for EC2 

**Scenario:** Your web application runs on EC2 instances. These instances need the permissions from your custom policy.

**Your task:**
- Create an IAM role named `WebServerRole-[yourname]`
- This role should be assumable by EC2 instances
- Attach your custom policy from Task 3 to this role

**What to submit:**
- Screenshot of the role summary page
- Screenshot of the trust relationships tab (what service can assume this role?)
- Screenshot showing your custom policy is attached

---

### Task 5: Test User Permissions 

**Your task:** Verify that your groups are working correctly.

**Test the db-admin user:**
- Log in as this user (use incognito/private window)
- Try to access RDS console - should WORK
- Try to access other services - should FAIL or have limited access
- Take screenshots of successes and failures

**Test the dev-junior user:**
- Log in as this user (use different incognito window)
- Try to view CloudWatch Logs - should WORK
- Try to access RDS, EC2, or other services - should FAIL
- Take screenshots of successes and failures

**What to submit:**
- Screenshots showing successful access to allowed services
- Screenshots showing denied access to restricted services
- For EACH user (minimum 4 screenshots total)

---

### Task 6: Test Role on EC2 

**Your task:** Verify that your IAM role works correctly on an EC2 instance.

**Steps:**
1. Launch a t2.micro EC2 instance
2. Attach your IAM role to the instance
3. Connect to the instance (EC2 Instance Connect)
4. Verify the role is attached using the metadata service
5. Test the permissions by:
   - Creating an S3 bucket with the correct prefix (should work)
   - Creating a DynamoDB table with the correct prefix (should work)
   - Writing data to the DynamoDB table (should work)
   - Trying to create resources WITHOUT the correct prefix (should fail)
   - Trying to DELETE resources (should fail)

**What to submit:**
- Screenshot showing the role attached to your EC2 instance
- Screenshots of successful operations (with correct prefix)
- Screenshots of failed operations (wrong prefix or no delete permission)
- Explanation of why each operation succeeded or failed

---

### Task 7: Security Analysis 

Answer these questions in your submission:

**Q1:** Why did we create groups instead of attaching policies directly to users? What are the advantages?

**Q2:** Your custom policy restricts resources to the `webapp-*` prefix. Explain why this is important and give a real-world example of damage this could prevent.

**Q3:** What would happen if you tried to attach your `WebServerRole` to a Lambda function? Would it work? Why or why not?

**Q4:** The DatabaseAdmin group has "FullAccess" to RDS. Is this following the Principle of Least Privilege? How could you make it more restrictive?

**Q5:** Explain the difference between these two ARNs:
   - `arn:aws:s3:::my-bucket`
   - `arn:aws:s3:::my-bucket/*`

**Q6:** Your EC2 instance has been running for 3 hours. The role's temporary credentials expire after 1 hour. Is the EC2 still able to access AWS services? Explain the mechanism.

**Q7:** Security incident: An attacker has compromised your EC2 instance and is using the role to access S3. What should you do IMMEDIATELY to cut off their access?
   - A) Delete the EC2 instance
   - B) Revoke the IAM role's active sessions
   - C) Change the S3 bucket policy
   - D) Delete the user's access keys

   Choose one and explain your reasoning.

---

### Task 8: BONUS - Enable MFA 

**Your task:**
- Enable MFA (Multi-Factor Authentication) on both IAM users
- Use a virtual MFA device (Google Authenticator or Authy)
- Test that MFA is required when logging in

**What to submit:**
- Screenshots showing MFA enabled for each user
- Screenshot of the MFA login prompt

---

### Task 9: Cleanup 

**Delete ALL resources you created to avoid charges:**
- DynamoDB tables
- S3 buckets (must empty them first!)
- EC2 instance
- IAM users
- IAM groups  
- IAM role
- Custom policy

**What to submit:**
- Screenshots proving all resources have been deleted

---

## 📝 Submission Instructions

### 1. Fork This Repository

Click the "Fork" button on GitHub

### 2. Clone Your Fork
```bash
git clone https://github.com/YOUR-USERNAME/iam-security-assignment.git
cd iam-security-assignment
```

### 3. Create Your Submission Folder
```bash
mkdir -p submissions/YOUR-NAME/screenshots
cp SUBMISSION_TEMPLATE.md submissions/YOUR-NAME/README.md
```

### 4. Complete the Assignment

- Take screenshots and save to `submissions/YOUR-NAME/screenshots/`
- Fill out `submissions/YOUR-NAME/README.md`
- Name screenshots clearly: `task1-groups.png`, `task2-users.png`, etc.

### 5. Submit via Pull Request
```bash
git add .
git commit -m "Assignment submission - Your Name"
git push origin main
```

Then create a Pull Request on GitHub.

---


---

## 🚫 Rules

- ❌ Do NOT copy policies from the internet without understanding them
- ❌ Do NOT share your work with other students  
- ❌ Do NOT commit AWS credentials to GitHub
- ✅ You MAY use AWS documentation
- ✅ You MAY use the IAM Policy Simulator to test
- ✅ You MAY ask clarifying questions

---

## 💡 Resources

**AWS Documentation:**
- IAM Users and Groups: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html
- IAM Roles: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html
- IAM Policies: https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html
- Policy Reference: https://docs.aws.amazon.com/service-authorization/latest/reference/

**Useful Tools:**
- IAM Policy Simulator: https://policysim.aws.amazon.com/
- Policy Generator: https://awspolicygen.s3.amazonaws.com/policygen.html

**Review Your Class Notes!**

---

## ⏰ Time Estimate

- Total: 2-3 hours
- If you're spending more than 4 hours, reach out for help!

---

**Good luck! This assignment tests everything you learned about IAM. Show me what you know! 🚀**

**Instructor:** Sarlynoel Ndzie Dighambong

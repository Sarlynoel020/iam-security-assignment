# IAM Assignment Submission

**Student Name:**  
**Date:**  
**Time Spent:**

---

## Task 1: IAM Groups

### Screenshots
- [ ] Groups list
- [ ] DatabaseAdmins permissions
- [ ] JuniorDevelopers permissions

### Notes


---

## Task 2: IAM Users

### Screenshots
- [ ] Users list
- [ ] db-admin group membership
- [ ] dev-junior group membership

### Notes


---

## Task 3: Custom Policy

### Screenshots
- [ ] Policy in IAM console
- [ ] Policy JSON view

### Your Policy JSON
```json
{
  "Version": "2012-10-17",
  "Statement": [
    // YOUR POLICY HERE
  ]
}
```

### Explanation
Why did you choose these specific actions and resources?


---

## Task 4: IAM Role

### Screenshots
- [ ] Role summary
- [ ] Trust relationships
- [ ] Attached policies

### Notes


---

## Task 5: User Permission Tests

### db-admin User
- [ ] Successful RDS access
- [ ] Denied access to another service

### dev-junior User
- [ ] Successful CloudWatch access
- [ ] Denied access to another service

### Observations


---

## Task 6: EC2 Role Tests

### Screenshots
- [ ] Role attached to EC2
- [ ] Successful operations (with correct prefix)
- [ ] Failed operations (wrong prefix or delete)

### Explanation
Why did each operation succeed or fail?


---

## Task 7: Security Questions

**Q1: Why use groups vs direct policy attachment?**

**Answer:**


**Q2: Why restrict to webapp-* prefix?**

**Answer:**


**Q3: Can WebServerRole be used by Lambda?**

**Answer:**


**Q4: Is DatabaseAdmin "FullAccess" least privilege?**

**Answer:**


**Q5: Difference between bucket ARN and bucket/* ARN?**

**Answer:**


**Q6: How do credentials auto-rotate?**

**Answer:**


**Q7: EC2 compromised - what to do? (A/B/C/D)**

**Answer:**

**Reasoning:**


---

## Task 8: BONUS - MFA

### Screenshots
- [ ] MFA on db-admin
- [ ] MFA on dev-junior
- [ ] MFA login prompt

### Notes


---

## Task 9: Cleanup

### Screenshots
- [ ] Users deleted
- [ ] Groups deleted
- [ ] Role deleted
- [ ] Policy deleted
- [ ] EC2 terminated

---

## Reflection

**Most challenging part:**

**What I learned:**

**What I'd do differently in production:**

---

**Submission Checklist:**
- [ ] All screenshots included
- [ ] All questions answered
- [ ] Policy JSON included
- [ ] No credentials visible
- [ ] Resources cleaned up

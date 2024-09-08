# **AWS IAM Study Notes**

### **Overview**
AWS Identity and Access Management (IAM) allows you to securely control access to AWS resources. It helps manage permissions through users, groups, roles, and policies.

---

## **Key Concepts**

### **Users**
- Represents individual people or applications.
- Assigned permissions via policies to access AWS resources.
- Each user has unique credentials (passwords, access keys).

### **Groups**
- Collection of IAM users.
- Permissions assigned to the group apply to all its members.
- Simplifies permissions management across multiple users.

### **Roles**
- Delegate access to AWS services with temporary credentials.
- Commonly used for cross-account access and services (e.g., EC2 accessing S3).
- No permanent credentials are involved.

### **Policies**
- JSON documents that define permissions.
- Types of Policies:
  - **Managed Policies**: Created and managed by AWS or users.
  - **Inline Policies**: Attached directly to a user, group, or role.
  - **Permission Boundaries**: Limits the maximum permissions.
- Define which actions are allowed or denied on specific resources.

---

## **Authentication and Security**

### **Passwords**
- IAM users require passwords for console access.
- You can enforce password policies (complexity, expiration, reuse prevention).

### **Multi-Factor Authentication (MFA)**
- Adds an additional layer of security with a second factor like a one-time code.
- Can be enforced for users and accounts handling sensitive tasks.

---

## **Best Practices**

1. **Principle of Least Privilege**: Grant only necessary permissions.
2. **Use Roles for Service Access**: Avoid embedding credentials in code by using IAM roles.
3. **Enable MFA**: Enforce MFA for root accounts and sensitive operations.
4. **Regularly Review Permissions**: Audit and adjust permissions periodically.
5. **Use AWS Organizations**: Manage multi-account setups with centralized control using Service Control Policies (SCPs).

---

## **IAM Tools**

### **Credentials Report**
- Provides a downloadable list of all IAM users and the status of their credentials (e.g., passwords, access keys). Useful for auditing inactive or outdated credentials.

### **Access Advisor**
- Shows the last time an IAM user or role accessed a service. It helps identify users or roles with permissions they no longer need.

### **IAM Policy Simulator**
- A tool for testing policies. It validates whether a user, group, or role has the correct permissions before you apply them.

---


# **AWS IAM Organizations**

### **Overview**
AWS Organizations enables central management of multiple AWS accounts. It simplifies governance, billing, and security for large setups.

---

## **Key Concepts**

### **Consolidated Billing**
- Combine billing for multiple accounts under one master account.
- Allows for shared volume discounts and easy billing management.

### **Organizational Units (OUs)**
- Group accounts for hierarchical management.
- Apply policies to groups rather than individual accounts.

### **Service Control Policies (SCPs)**
- Apply permission boundaries across accounts and OUs.
- Ensure accounts can't perform actions outside the set policies.

### **Account Management**
- Automate the creation of new accounts.
- Centralize management and governance for easier scaling.

### **Cross-Account Access**
- Simplifies sharing resources between accounts.
- Improves security with centralized control.

---

## **Best Practices**
- Use **SCPs** to enforce security policies globally.
- Structure accounts based on functional needs with **OUs**.
- Use **Consolidated Billing** to manage costs efficiently.

---

AWS Organizations is vital for multi-account environments, enabling centralized control and consistent governance.

# **AWS IAM Policies**

### **Overview**
IAM policies are JSON-based documents used to define permissions to control access to AWS resources. They specify what actions are allowed or denied on specific resources.

---

## **Key Concepts**

### **Policy Structure**
- **Version**: The policy language version (usually “2012-10-17”).
- **Statement**: Main component, includes:
  - **Effect**: "Allow" or "Deny."
  - **Action**: Specifies AWS actions (e.g., `s3:PutObject`).
  - **Resource**: Defines resources (e.g., ARNs).
  - **Condition**: Optional restrictions (e.g., IP address, time).

## **Types of Policies**

1. **Managed Policies**: 
   - Reusable policies managed by AWS or users.
   - Can be applied to multiple users, groups, and roles.

2. **Inline Policies**: 
   - Directly attached to a single user, group, or role.
   - Offers more granular control but is harder to manage at scale.

3. **Service Control Policies (SCPs)**:
   - Applied at the organization or account level in AWS Organizations.
   - Set permission boundaries for all accounts and resources under AWS Organizations.

4. **Permission Boundaries**: 
   - Limits maximum permissions that a user or role can have.
   - Useful for ensuring users/roles don’t have broader permissions than necessary.

5. **Session Policies**: 
   - Temporary policies attached to an IAM role session.
   - Allows further restriction of permissions beyond what's already allowed.

## **Key IAM Policy Features**

- **Policy Evaluation Logic**: AWS evaluates policies using an explicit deny and allow model. If no explicit "Allow" is found, actions are implicitly denied.
- **Policy Variables**: You can use variables like `${aws:username}` to create dynamic, flexible policies.
- **Conditions**: Can use conditions to restrict access (e.g., time-based access, IP addresses).

## **Best Practices**

1. **Principle of Least Privilege**: Always grant the minimal necessary permissions.
2. **Use Managed Policies**: Whenever possible, use managed policies to simplify management.
3. **Policy Auditing**: Regularly review and update policies to ensure they reflect current access needs.
4. **Monitoring**: Use IAM tools like **Access Advisor** and **Credential Reports** to audit permissions and activity for users/roles.

## **Example**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::example-bucket/*"
        }
    ]
}
```

# **Policy Evaluation Logic**

### **Overview**
AWS evaluates requests against IAM policies by following specific logic to determine whether actions are allowed or denied.

## **Key Steps in Policy Evaluation**

1. **Default Deny**: All actions are denied unless explicitly allowed.
2. **Explicit Allow**: Actions explicitly allowed in a policy are permitted unless an explicit deny exists.
3. **Explicit Deny**: Any action explicitly denied in a policy overrides any allow.

### **Additional Details**

- **Conditions**: Policies can include conditions that further refine access, such as time-based or IP restrictions.
- **Multiple Policies**: AWS evaluates all identity-based, resource-based, and organization-level policies.

## **Key Takeaways**
- **Explicit Deny** always takes precedence.
- Policies with conditions refine access further.
- All relevant policies (attached to users, groups, roles, or resources) are evaluated together.

# **AWS IAM Identity Center (formerly AWS SSO)**

### **Overview**
AWS IAM Identity Center simplifies access management for multiple AWS accounts using a single set of credentials. It provides centralized access and integrates seamlessly with AWS Organizations.

---

## **Key Features for Solutions Architect – Associate Exam**

- **Single Sign-On (SSO)**: Centralized login across multiple AWS accounts.
- **Permission Sets**: Define and assign AWS-specific permissions to users or groups.
- **Integration with AWS Organizations**: Manage access across multiple accounts.

---

## **Exam-Relevant Details**

- Focus on **Permission Sets** and **SSO** integration with AWS Organizations.
- Streamlines access management for large-scale AWS environments.

# **AWS Control Tower**

### **Overview**
AWS Control Tower simplifies setting up and governing secure multi-account AWS environments, known as **landing zones**.

---

### **Key Features for Solutions Architect – Associate Exam**
- **Automated Setup**: Creates a secure, multi-account AWS environment.
- **Guardrails**: Enforces security, compliance, and governance.
- **Integration with AWS Organizations**: Manage multiple accounts easily.

---

# **AWS Directory Service**

### **Overview**
AWS Directory Service enables the use of **Microsoft Active Directory (AD)** on AWS, managing users, groups, and devices.

---

### **Key Features for Solutions Architect – Associate Exam**
- **AWS Managed Microsoft AD**: Full-featured, scalable AD on AWS.
- **AD Connector**: Connect AWS services to an on-premises AD.

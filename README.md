# cyber-day-18

# Day 18: Basics of Cyber Security

## Authentication & Authorization

### What is the Difference Between Authentication & Authorization?

Authentication and Authorization are both important processes in access control and identity management that determine the security of a system. 

- **Authentication** verifies a user's identity.
- **Authorization** determines what access a user has.

For example, when you go through airport security:
- You show your ID to authenticate your identity.
- When you get to the gate, you present your boarding pass to authorize you to board the plane.

## What are the Characteristics of a Good Password Policy?

A good password policy encourages users to create and use strong passwords, which can help protect systems and data from attacks.

1. **Length**: A minimum of 12 characters, but 14 or more is better.
2. **Multi-factor Authentication**: Requiring a second factor for authentication, such as a security question.
3. **Complexity**: A combination of uppercase and lowercase letters, numbers, and symbols.
4. **Uniqueness**: Never reusing passwords across multiple accounts.
5. **Account Lockout**: Limiting the number of invalid password attempts before locking out the account.

# Testing the Effectiveness of a Deployed Password Policy

Testing the effectiveness of a password policy is crucial to ensure security. Here are some ways to test a deployed password policy:

## Character Set and Complexity Testing
- Verify that the application enforces the use of different character types, including uppercase, lowercase, digits, and special symbols.

## Brute Force Testing
- Assess the application's resistance to brute force attacks using available password dictionaries to guess passwords.

## Common Passwords and Forbidden Information
- Test if common passwords (e.g., "password1", "123456") are allowed.

# Two-Factor Authentication (2FA)

## What is Two-Factor Authentication?
Two-factor authentication (2FA) is an access identity and management security method that requires two forms of identification to access resources and data.

## Why Do We Need 2FA?
- **Protects Sensitive Data**: Financial, healthcare, and other sensitive information are better protected.
- **Mitigates Password Vulnerabilities**: Reduces the risk associated with compromised passwords.
- **Balances Privacy and Security**: Provides an additional layer of security without overly compromising user privacy.
# Mitigations to Prevent Brute Force Attacks

Brute force attacks are a common threat, but there are several effective techniques to prevent them:

## Account Lockouts
- Implement a policy that locks out an account after a certain number of incorrect password attempts.

## Make the Boot User Inaccessible via SSH
- Modify default settings to restrict SSH access to critical system users.

## Use CAPTCHA
- Implement CAPTCHA to prevent automated login attempts.

## Limit Logins to a Specified IP Address or Range
- Restrict login access to known and trusted IP addresses.

## Employ Two-Factor Authentication (2FA)
- Use 2FA to add an extra layer of security.

## Use Unique Login URLs
- Create unique URLs for login pages to obscure them from attackers.

## Monitor Your Server Logs
- Regularly check server logs for suspicious activities.

# Impacts of Parameter Manipulation/Tampering

Parameter tampering, also known as parameter manipulation, is a web attack where an attacker modifies parameters exchanged between a client and a server to exploit the application.

## Potential Impacts
- **Unauthorized Access**: Gaining access to restricted areas.
- **Privilege Escalation**: Attacker gains higher level permissions.
- **Data Corruption**: Integrity of data is compromised.
- **Financial Fraud**: Manipulating financial transactions for gain.
- **System Disruption**: Causing parts of the application to fail.
- **Sensitive Data Exposure**: Leaking confidential information.
- **Modification of Application Behavior**: Altering how the application functions.

# Differences Between Horizontal, Vertical & Context-Based Access Control

## Vertical Access Control

**Definition**: Vertical access control restricts access to sensitive functionality based on different roles or types of users.

- **Example**: In a web application, an administrator might have the right to modify or delete user accounts, whereas an ordinary user does not have this privilege.

## Horizontal Access Control

**Definition**: Horizontal access control restricts access to resources or features to specific users at the same permission level.

- **Example**: In a banking application, a user can view transactions and make payments from their own accounts but cannot access the accounts of any other user.

## Context-Based Access Control

**Definition**: Context-based access control restricts access based on the state of the application or the user's interaction with it.

- **Example**: A retail website might prevent users from modifying the contents of their shopping cart after making a payment.

## Summary of Differences

- **Vertical Access Control**: Different types of users have access to different functions.
- **Horizontal Access Control**: Different users have access to a subset of resources of the same type.
- **Context-Based Access Control**: Access restrictions depend on the application's state and the user's interaction.

# Scenario: Accessing Admin Dashboard by Parameter Manipulation

## Vulnerability Present in the Application

In this scenario, the application has an **Insecure Direct Object References (IDOR)** vulnerability.

### What is IDOR?

IDOR occurs when an attacker can manipulate parameters, such as URLs or form fields, to access resources they are not authorized to access.

- **Example**: In your case, you gained access to the admin's account dashboard by altering the parameter in the URL.

### Impacts of IDOR

- **Unauthorized Access**: Gaining access to sensitive data.
- **Modification or Deletion of Information**: Altering information meant for other users.
- **Various Security Breaches**: Exploiting the application further due to inadequate access controls.

### Mitigation

- **Always Validate User Input**: Ensure proper authorization checks.
- **Use Indirect References**: Use unique tokens instead of exposing direct object references (e.g., database keys) in URLs.

## Type of Access Control Bypassed and Action Performed

### Access Control Bypassed

In the given scenario, you bypassed **horizontal access control** that should have restricted you, a user with normal privileges, from accessing the admin dashboard.

### Action Performed

You performed a **privilege escalation** by exploiting the IDOR vulnerability. 

- **Privilege Escalation**: You escalated your privileges from a normal user to an admin by manipulating the parameter to access the admin dashboard.

### Summary

- **Access Control Bypassed**: Horizontal Access Control
- **Action Performed**: Privilege Escalation

# Different Types of Privilege Escalation

Privilege escalation is a type of security breach where an attacker gains elevated access to resources that are normally protected from a user. There are two main types of privilege escalation: vertical and horizontal.

## 1. Vertical Privilege Escalation

**Definition**: Vertical privilege escalation, also known as privilege elevation, occurs when an attacker gains higher privileges than they are authorized to have. This usually involves gaining administrative or root-level access from a standard user account.

**Example**:
- **Web Application Vulnerability**: An attacker exploits a vulnerability in a web application to gain administrative access. For example, if a web application has a poorly protected administrative interface, an attacker might use SQL injection to bypass authentication and gain admin privileges.

## 2. Horizontal Privilege Escalation

**Definition**: Horizontal privilege escalation occurs when an attacker gains access to the same level of privileges they already have but from another user account. This type of attack is typically used to access data or resources belonging to other users.

**Example**:
- **Account Manipulation**: In a web application, an attacker manipulates the URL or parameters to access another user's account. For example, changing the user ID in the URL from "user_id=123" to "user_id=124" to view another user's account information.

## Summary

- **Vertical Privilege Escalation**: 
  - **Definition**: Gaining higher-level privileges (e.g., from user to admin).
  - **Example**: Using SQL injection to gain admin access.
- **Horizontal Privilege Escalation**:
  - **Definition**: Gaining access to the same level of privileges but for another user's account.
  - **Example**: Manipulating URL parameters to access another user's account.

### Importance of Mitigating Privilege Escalation

Implementing robust access controls, validating user input, and regularly auditing security measures are crucial to preventing both vertical and horizontal privilege escalation.

# Example: Session Hijacking

**Session Hijacking**: An attacker intercepts the session ID of another user through methods like cross-site scripting (XSS) or man-in-the-middle attacks. Once the session ID is obtained, the attacker can impersonate the other user and access their account without needing higher privileges.

## Difference Between IDOR and Missing Function Level Access Control (MFLAC)

### IDOR (Insecure Direct Object References)

**Definition**: IDOR occurs when an application allows direct access to objects based on user-supplied input without proper authorization checks.

**Characteristics**:
- Related to direct object access.
- Exploits a lack of authorization checks for specific resources.
- Allows attackers to manipulate input values to access unauthorized resources.

**Example**: 
An application allows users to view their invoices via a URL like:



# Example: Session Hijacking

**Session Hijacking**: An attacker intercepts the session ID of another user through methods like cross-site scripting (XSS) or man-in-the-middle attacks. Once the session ID is obtained, the attacker can impersonate the other user and access their account without needing higher privileges.

## Difference Between IDOR and Missing Function Level Access Control (MFLAC)

### IDOR (Insecure Direct Object References)

**Definition**: IDOR occurs when an application allows direct access to objects based on user-supplied input without proper authorization checks.

**Characteristics**:
- Related to direct object access.
- Exploits a lack of authorization checks for specific resources.
- Allows attackers to manipulate input values to access unauthorized resources.

**Example**: 
An application allows users to view their invoices via a URL like:
https://example.com/invoice?id=12345
If the application does not verify that the current user owns invoice 12345, an attacker can change the `id` parameter to another value to access other users' invoices.

### Missing Function Level Access Control (MFLAC)

**Definition**: MFLAC occurs when an application does not properly enforce access control to various functions or actions based on the user's role or permissions.

**Characteristics**:
- Related to function or action access.
- Exploits lack of proper access control checks for specific actions.
- Allows attackers to invoke functions or perform actions they should not have access to.

**Example**:
An application has an admin interface accessible at:

https://example.com/admin

This interface includes functions like user management and configuration settings. If the application does not check whether a user has administrative privileges before allowing access to these functions, any authenticated user can access and perform admin-level actions.

## Summary of Differences

- **IDOR**:
  - **Focus**: Direct object access.
  - **Vulnerability**: Lack of authorization checks for accessing specific resources.
  - **Example**: Accessing another user's invoice by changing the `id` parameter.

- **MFLAC**:
  - **Focus**: Function or action access.
  - **Vulnerability**: Lack of proper access control checks for specific actions.
  - **Example**: Accessing admin functionalities without proper administrative privileges.

### Importance of Mitigating IDOR and MFLAC

Implementing robust authorization checks, validating user input, and enforcing strict role-based access controls are crucial to preventing both IDOR and MFLAC vulnerabilities.
# Difference Between IDOR and Missing Function Level Access Control (MFLAC)

## Focus
- **IDOR**: Focuses on the improper access of objects (data).
- **MFLAC**: Focuses on the improper access of application functions or actions.

## Exploitation Method
- **IDOR**: Exploited by manipulating object identifiers to access unauthorized data.
  - **Example**: Changing the parameter in a URL to access another user's invoice, like:
    ```
    https://example.com/invoice?id=12345
    ```
- **MFLAC**: Exploited by accessing application endpoints directly without proper function-level authorization checks.
  - **Example**: Accessing an admin URL to delete a user without having admin privileges, like:
    ```
    https://example.com/admin/delete_user?id=123
    ```

# Mitigating Broken Access Control

**Broken Access Control** refers to security vulnerabilities where authenticated users are allowed to access unauthorized functionality or data. Attackers exploit these vulnerabilities to gain unauthorized access. Mitigating broken access control involves a combination of proper design, implementation, and ongoing management practices.

## Mitigation Strategies

### 1. Implement Role-Based Access Control (RBAC)
- **Define Roles and Permissions**: Clearly define roles and their associated permissions.
- **Enforce Role Checks**: Ensure that the application consistently checks the user's role before granting access to sensitive functions.

### 2. Use Secure Coding Practices
- **Indirect Object References**: Use indirect references, such as unique tokens, instead of direct object references (e.g., database keys) in URLs.
- **Input Validation**: Validate all user inputs to ensure they conform to expected formats and do not contain malicious data.

### 3. Implement Context-Aware Access Control
- **Attribute-Based Access Control (ABAC)**: Use attributes (e.g., user role, time of access, location) to make dynamic access control decisions.
- **Dynamic Access Decisions**: Implement access controls that adapt to the context of the request, ensuring that access permissions are evaluated in real-time based on the current state of the application and user.

## Summary

Mitigating broken access control vulnerabilities requires a multi-faceted approach:
- **Role-Based Access Control (RBAC)**: Define roles and permissions, enforce role checks.
- **Secure Coding Practices**: Use indirect object references and validate user input.
- **Context-Aware Access Control**: Implement ABAC and dynamic access decisions.

By combining these strategies, you can significantly reduce the risk of unauthorized access and protect your application from common security vulnerabilities.

# Enforcing Server-Side Access Controls

## Enforce Server-Side Checks
- **Consistent Enforcement**: Ensure that access controls are enforced consistently on the server-side for all requests, regardless of the source.

## Auditing and Logging
- **Comprehensive Logging**: Implement detailed logging of all access attempts and actions, especially those involving sensitive data or functions.
- **Regular Audits**: Conduct regular audits of logs to detect and respond to suspicious activities or anomalies.

## Security Testing and Code Reviews
- **Automated Tools**: Utilize automated security testing tools to identify potential vulnerabilities in the code.
- **Manual Code Reviews**: Conduct manual code reviews to ensure security best practices are followed.
- **Penetration Testing**: Perform regular penetration testing to identify and fix security weaknesses.

## Implement Multi-Factor Authentication (MFA)
- **Multi-Factor Authentication**: Require multiple forms of verification (e.g., password and mobile OTP) to enhance security.

## Use Security Frameworks and Libraries
- **Trusted Libraries**: Use well-established and trusted security frameworks and libraries.
- **Regular Updates**: Regularly update libraries and frameworks to incorporate the latest security patches and improvements.

# Summary

Mitigating broken access control and enforcing server-side security involves a comprehensive approach:

- **Server-Side Checks**: Ensure consistent enforcement of access controls.
- **Auditing and Logging**: Implement comprehensive logging and conduct regular audits.
- **Security Testing and Code Reviews**: Use automated tools, manual reviews, and penetration testing to identify and fix vulnerabilities.
- **Multi-Factor Authentication (MFA)**: Enhance security by requiring multiple forms of verification.
- **Security Frameworks and Libraries**: Use and regularly update trusted libraries and frameworks to maintain security.

By implementing these practices, you can significantly enhance the security of your application and protect against unauthorized access.
```

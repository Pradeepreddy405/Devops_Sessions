## Authentication and Authorization in Cloud & DevOps

Modern cloud and DevOps systems are highly distributed, automated, and exposed over networks. In such environments, security is not just about protecting user logins—it’s about controlling identities and access across humans, services, and infrastructure.

 - At the core of this security model are two fundamental concepts:
 - Authentication
 - Authorization
 
## Authentication vs Authorization (Core Difference)
 - Authentication → Who are you?
 - Authorization  → What are you allowed to do?



Example:
 - You log into a cloud console it defines "Authentication "
 - You can only view resources but not delete them (or) at what level you could use them defines "Authorization"


Authentication is the process of verifying identity. In modern systems, identities are not just humans, they include applications, services, containers, and pipelines.

---

### 1. Human Authentication

This is the traditional entry point.

Common Methods:
Username + Password
Multi-Factor Authentication (MFA)
Single Sign-On (SSO)
SSO in Practice:

With SSO, a user logs in once via an identity provider and gains access to multiple systems without re-authenticating.

Example:
A developer logs in via corporate SSO → accesses cloud console on Amazon Web Services or Microsoft Azure

---

### 2. Machine-to-Machine Authentication (Critical in DevOps)

This is where real systems operate.

In DevOps, services constantly communicate with each other without human involvement.

Common Mechanisms:
API Tokens
Service Accounts
IAM Roles
Short-lived credentials

Example: 
 - A CI/CD pipeline deploys code to cloud infrastructure without storing any passwords.

---

### 3 Core Authentication Mechanisms
 - Identity and Access Management (IAM)
 - IAM is the backbone of cloud authentication.

 - Centralized identity management
 - Defines users, roles, and permissions
 - Strongly used in Amazon Web Services IAM
 #### Key Principle:
 - Assign roles, not direct permissions
 - This reduces risk and improves scalability.

---

### 4 Token-Based Authentication

Modern systems avoid passwords during communication.

Instead, they use tokens.

Popular Standards:
OAuth 2.0
OpenID Connect
How It Works:
User logs in
Server issues a token (e.g., JWT)
Client uses token for API requests
Why It Matters:
Tokens expire → reduces risk
No need to send credentials repeatedly

---

### 5 SSH Key-Based Authentication
 - Used for secure server access.
 - Public/private key pair
 - No password required
 - Standard in Linux-based environments
 - Essential for DevOps engineers

---

### 6 API Keys (Use Carefully)
 - Simple authentication method
 - Often used for external integrations

 #### Risk
 - If leaked, they can be abused easily.

 #### Best Practice:
 - Rotate regularly
 - Restrict permissions
 - Authentication in CI/CD Pipelines
 - CI/CD pipelines must access infrastructure securely.
 - Tools like Jenkins should never store plain credentials.

 #### Best Practices:
 - Use IAM roles instead of static keys
 - Store secrets in secure vaults
 - Use temporary credentials

### Example Flow : Jenkins job → assumes IAM role → deploys resources → credentials expire automatically

---

### 7 Secrets Management
Secrets include:
- API keys
- Database passwords
- Tokens
Tools:
- HashiCorp Vault
- AWS Secrets Manager
- Kubernetes Secrets
- Golden Rule: Never store secrets in code or Git repositories

---

### 8 Cloud-Native Authentication
- AWS Example
- IAM Users (avoid for production workloads)
- IAM Roles (preferred)
- STS (temporary credentials)

 #### Kubernetes Example
 - Using Kubernetes:
 - Service Accounts → identity for pods
 - RBAC → access control

#### Example: A pod accesses AWS resources using IAM role → no hardcoded credentials

---

### 9 How Authentication and Authorization works in DevOps & Cloud 

Once identity is verified, authorization decides access.


 #### Role-Based Access Control (RBAC)
 - Assign roles to users/services
 - Roles define permissions

 - Example:
 - Developer → read access
 - Admin → full access

 Used in:
 - Kubernetes
 - Cloud IAM systems
 - Policy-Based Access
 - Permissions are defined using policies.

 Example in AWS:

 JSON policies define allowed/denied actions
 - follows "Principle of Least Privilege"
 - Give only the minimum access required.

 This reduces:
 - Security risks
 - Blast radius of failures

---
 
### 10 Zero Trust Security Model

Modern systems assume no implicit trust.
Every request must be:
 - Authenticated
 - Authorized
 - Even internal services must verify identity.

---

### 11 End-to-End Flow
 - User logs in via SSO
 - Identity provider issues token
 - User accesses application
 - Application validates token
 - Backend services authenticate using service identities
 - Infrastructure access controlled via IAM roles
 #### Common Mistakes
  - Storing secrets in Git
  - Using long-lived credentials
  - Giving excessive permissions
  - Ignoring machine authentication
  - Confusing authentication with authorization

 #### Most real-world breaches happen because of:
  - Poor secrets management
  - Misconfigured IAM roles
  - Over-permissioned access
  - Not because of weak passwords.

### Summary

 - Authentication and authorization are the foundation of secure DevOps systems.
 - Authentication verifies identity
 - Authorization controls access
 - Modern systems rely on tokens, roles, and short-lived credentials
 - Security is enforced across humans, services, and infrastructure
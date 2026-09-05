# Secure Cloud Architecture Plan

## Architecture

Users  
↓  
CDN  
↓  
Load Balancer  
↓  
Application Servers  
↓  
Private Database

## CDN

The CDN stores cached copies of static content closer to users to improve loading speed.

## Load Balancer

The load balancer distributes incoming requests across multiple application servers.

## Application Servers

Application servers process requests from users. These servers should be placed in a private subnet.

## Database

The database stores student records. The database should remain private and should not be directly accessible from the Internet.

---

# Public and Private Resources

| Resource           | Public or Private | Explanation |
|--------------------|-------------------|-------------|
| CDN                | Public            | The CDN provides cached content to users through the Internet. |
| Load Balancer      | Public            | The load balancer receives incoming requests from users. |
| Application Server | Private           | Application servers process requests and should not be directly accessible from the Internet. |
| Database           | Private           | The database stores student records and should not be directly accessible from the Internet. |

---

# Security Controls

## IAM

Only authorized users should have access to the cloud environment. Users should receive permissions based on their responsibilities.

## MFA

Administrator accounts should use Multi-Factor Authentication (MFA) to provide an additional layer of security.

## Firewall / Security Group

| Connection                         | Action  | Reason |
|------------------------------------|---------|--------|
| Internet → Load Balancer           | Allowed | Users need to access the application. |
| Load Balancer → Application Server | Allowed | The load balancer needs to send requests to the application servers. |
| Application Server → Database      | Allowed | The application servers need to access student records. |
| Internet → Database                | Blocked | The database must remain private. |

## Encryption

Student information should be encrypted to protect it from unauthorized access.

## Logging

Important activities such as login attempts, permission changes, and access to resources should be recorded.

## Monitoring

Suspicious activities such as unauthorized access attempts, unusual login activity, and unexpected traffic should be monitored.

## Backup

The database should have backups so student records can be recovered if data is lost, deleted, or corrupted.

---

# Principle of Least Privilege

The principle of least privilege means that each user should only receive the access necessary to perform their responsibilities.

| User          | Allowed Access |
|---------------|----------------|
| Administrator | Manage the system, cloud resources, users, and security settings. |
| Instructor    | View and manage student information needed for instructional responsibilities. |
| Student       | View permitted student information. |
| Developer     | Access application development resources needed for development and maintenance. |

Administrator access should not be given to everyone.

---

# Shared Responsibility Model

| Responsibility          | Cloud Provider or Customer | Explanation |
|-------------------------|----------------------------|-------------|
| Physical data center    | Cloud Provider              | Protects and manages the physical data center. |
| Physical servers        | Cloud Provider              | Manages the physical servers used for cloud services. |
| User accounts           | Customer                    | Manages application users and their accounts. |
| Student data            | Customer                    | Protects the student information stored in the application. |
| IAM permissions         | Customer                    | Determines which users receive specific permissions. |
| Application security    | Customer                    | Secures the application created and operated by the customer. |
| Database access rules   | Customer                    | Controls who and what can access the database. |
| Backups                 | Customer                    | Ensures important application data is backed up. |

## 1. What does Security OF the Cloud mean?

Security OF the Cloud means the security responsibilities handled by the cloud provider. This includes protecting the physical data center and physical servers.

## 2. What does Security IN the Cloud mean?

Security IN the Cloud means the customer's responsibility for protecting the resources and data placed in the cloud. This includes user accounts, student data, IAM permissions, application security, and database access rules.

---

# Architecture Questions

## 3. Which resource should be directly accessible from the Internet?

The load balancer should be directly accessible from the Internet because it receives incoming requests from users and forwards them to the application servers.

## 4. Why should the database remain private?

The database should remain private because it stores student records. Keeping it private reduces the risk of unauthorized access.

## 5. Why should users not connect directly to the database?

Users should not connect directly to the database because this would expose the database to unnecessary security risks. Users should access the application instead.

## 6. What is the purpose of a load balancer?

The purpose of a load balancer is to distribute incoming requests across multiple application servers.

## 7. What happens if one application server fails?

If one application server fails, the load balancer can send requests to another available application server so the application can continue operating.

## 8. What is the purpose of a CDN?

The purpose of a CDN is to store cached copies of static content closer to users to improve loading speed.

## 9. Why should administrator accounts use MFA?

Administrator accounts should use MFA because administrators have powerful permissions. MFA provides an additional layer of protection if a password is compromised.

## 10. Why should administrator access not be given to every employee?

Administrator access should not be given to every employee because it provides powerful permissions that are not necessary for most employees. Limiting administrator access reduces security risks.

## 11. Why are logging and monitoring important?

Logging and monitoring are important because they help identify suspicious activities, unauthorized access attempts, and other potential security problems.

## 12. Why are backups important?

Backups are important because they allow student records and other important data to be recovered if data is lost, deleted, or corrupted.
```

# Security

## Overview

This document will explain the network security measures implemented in the futsal web booking deployment process.

Security configuration will focus on network access control, remote administration security, application configuration protection, file permission management, and enabling encrypted HTTPS communications.

## Firewall Configuration

UFW (uncomplicated firewall) is used to control which network ports will be used as entry points to crucial parts such as Apache, SSH, and https.

### Allowed Services

| Port | Service | Purpose |
|------|---------|---------|
| 80 | HTTP | Web access |
| 443 | HTTPS | Secure web access |
| 4240 | SSH | Remote administration |

## SSH Hardening

As previously explained, SSH access is strengthened by replacing the default port with a custom port.

The firewall configuration is updated as needed to ensure that remote administration remains available through the new SSH port.

## File Permissions 

File ownership and permissions are configured to allow the Apache web server to access the Laravel application while maintaining appropriate file system restrictions.

The permission settings allow Apache to access the application and Laravel to write to directories that require write access, here is an example:

```hash
storage
bootstrap/cache
```

### Application Ownership

Laravel application files are provided to the web server user to ensure that Apache can access the application and directories needed for writing.

## Environment Security

The Laravel framework's environment configuration is managed through the `.env` file.

This file contains sensitive application and database configurations and cannot be uploaded to public repositories due to the risk of security issues.

Sensitive values ​​such as application keys and database credentials are excluded from version control.

## HTTPS & SSL/TLS

HTTPS is enabled using an SSL/TLS certificate configured for the application's public domain.

The certificate encrypts communications between the client and the application in use and provides secure HTTPS access to the Laravel application.

## Security Validation 

The implemented security configuration is now validated to ensure that required services remain accessible to users in general, while unnecessary network frequencies are restricted.

The validation included:

- Firewall rule verification
- SSH remote access verification
- Application file permission verification
- HTTPS connectivity verification
- Protection of sensitive environment configuration

## Security Improvements

The initial implementation was reviewed after the application was deployed to the server.

During the review, it was identified that server access was primarily performed using the superuser account. A dedicated administrative user with limited access rights was not created during the initial implementation.

This was identified as a security improvement for future implementations.

### Dedicated Administrative User

For routine user administration processes, it's best to use a new user other than the superuser. This user should only be granted specific access rights, depending on the purpose.

This user should only receive elevated access rights if necessary via sudo, while routine operations should be performed using a non-root account.

This approach aims to mitigate the worst-case scenario if the server is compromised, at least while it's still operating under a regular user, whose access is more limited than that of the superuser.

# Deployment Process

## Overview

This section of the document will explain the process of deploying a futsal booking website to an Ubuntu server.

The deployment was performed on a Virtual Private Server using Apache2 as the web server, PHP 8.2 as the runtime environment, and MySQL as the database server. The goal was to provide a stable production environment accessible through the public domain.

## Deployment Workflow

```text
Login to VPS
        │
        ▼
Update System Packages
        │
        ▼
Install Server Components
        │
        ▼
Upload Project via SCP
        │
        ▼
Configure Laravel Environment
        │
        ▼
Initialize Database
        │
        ▼
Configure Apache VirtualHost
        │
        ▼
Configure Firewall
        │
        ▼
Validate Application
        │
        ▼
Harden SSH Configuration
        │
        ▼
Configure SSL Certificate
        │
        ▼
Final Validation
```

# Login to VPS

This deployment process begins by logging into the VPS via secure shell (SSH) using the obtained public IP.

By using the following command:

```bash
ssh username@server-IP
```

Example: 

```bash
ssh root@154.19.37.170
```
SSH provided secure remote access to the Ubuntu Server, allowing all deployment and server administration tasks to be performed from the local development machine.

# Update System Packages

Before installing the required software, the server packages were updated to ensure the latest package information and security updates were available.

The update process reduced the possibility of dependency conflicts during software installation and ensured compatibility with the deployment environment.

Example: 

```text
sudo apt-get update
sudo apt-get upgrade -y
```

# Install Server Component

The software components needed to run the application include the following:

- Apache2
- MySQL Server
- PHP 8.3
- Required PHP Extensions
- Composer
- Git

These components are important parts to support Laravel applications to run on the server.

### Apache2 

Apache2 is a type of open source web server that is stable and compatible with various application platforms, which here acts as the main web server that serves Laravel applications.

```bash
sudo apt install Apache2
sudo systemctl restart
```

### MySQL Server

MySQL Server was chosen as the database because of its resource-efficient and multi-user capabilities, as well as its security with a robust encryption system and data layers.

The database is used to store user-created accounts and other necessary data.

```bash
sudo apt install mysql-server -y
```

### PHP 8.3

PHP 8.2 and its required extensions were installed to execute the Laravel application.

```bash
sudo apt install apache2 php php-cli php-mbstring php-xml php-bcmath php-curl php-mysql unzip cur git -y
```

### Composer

Composer is needed to manage PHP packages used by the Laravel framework.

```bash
curl -sS https://getcomposer.org/installer | php
composer -v
```

# Upload Laravel Application

Once the server environment is fully prepared, the next step is to upload the project files to the VPS server using Secure Copy Protocol (SCP).

The project is uploaded as a compressed archive to simplify the transfer process and preserve the project structure during deployment.

## Create Project Directory

At this stage, the Laravel application is stored in a different directory from the existing default directory to differentiate and separate the system's default files from the project files that we add ourselves.

```bash
sudo mkdir /var/www/project.futsal
```

This directory served as the deployment location for the application and helped maintain a clean and organized server structure.

## Transfer Project Via SCP

Laravel application files are sent from windows local storage to ubuntu server using SCP.

```bash
scp "C:\Users\...\PAS.futsal.zip" root@server-ip:/var/www/project.futsal/
```

The project was transferred as a compressed archive to simplify the file transfer process.

## Ekstrak Project Archive

Once the project files are moved, the archive is extracted inside the deployment directory.

```bash
unzip PAS.futsal.zip
```

The extracted files formed the Laravel application structure used for the subsequent deployment configuration.

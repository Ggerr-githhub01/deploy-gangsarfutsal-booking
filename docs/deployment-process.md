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

## Login to VPS

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

## Update System Packages

Before installing the required software, the server packages were updated to ensure the latest package information and security updates were available.

The update process reduced the possibility of dependency conflicts during software installation and ensured compatibility with the deployment environment.

Example: 

```text
sudo apt-get update
sudo apt-get upgrade -y
```

## Install Server Component

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

## Upload Laravel Application

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

## Configure Laravel Environment

Once the Laravel application files are on the server, the next step is to configure the deployment environment which is managed through the Laravel `.env` file.

### Environment File 

The `.env` file is located in the same location as the laravel project, used to define environment-specific application settings.

The Configuration Included : 

- Application environtment
- Application key
- Database connection
- Database credentials

Sensitive configuration values were kept outside version control.

## Initialize Database

The Laravel application's `.env` file will connect to the MySQL database on the Ubuntu server.

The database initialization process included generating the Laravel application key, configuring the database connection through the `.env` file, and running the Laravel database migrations.

### Generate Application Key

Laravel application keys are generated using Artisan.

```bash
php artisan key:generate
```
The generated `APP_KEY` is stored in the `.env` configuration file and is used by Laravel for application encryption.

### Configure Database Connection 

Laravel database connection is configured via `.env` file to connect the application with MySQL database server.

The configured part include the following : 

```bash
DB_DATABASE
DB_USERNAME
DB_PASSWD
```
Database credentials are configured according to the MySQL database and user created during the server setup process.

### Run Database Migration

After the entire configuration process is complete, database initialization is performed by running Laravel migrations.

```bash
php artisan:migrate
```

The migration process created the database tables required by the Laravel application.

## Configure Apache Virtualhost

The Apache VirtualHost is configured to serve the Laravel application from its `public` directory.

The VirtualHost configuration defines the application's document root, directory access rules, and Apache log files.

### Create VirtualHost Configuration 

A custom VirtualHost configuration file has been created for the Laravel application.

```bash
sudo nano /etc/apache2/sites-available/futsal.conf
```

The configuration below points Apache to the Laravel application's `public` directory:

```bash
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/project.futsal/public

    <Directory /var/www/project.futsal>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/futsal_error.log
    CustomLog ${APACHE_LOG_DIR}/futsal_access.log combined
</VirtualHost>
```
#### noted: In the ServerAdmin section, it still contains localhost because this is taken from the project documentation that was practiced on virtual box, while the VPS and domain are no longer active.

## Enable Apache Configuration

Apache rewrite module has been enabled and Laravel VirtualHost has been activated.

```bash
sudo a2enmod rewrite
sudo a2ensite laravel.conf
sudo a2dissite 000-default.conf
```

After that restart the apache system to activate the new configuration.

```bash
sudo systemctl restart apache2
```

### Configuration Purpose

The VirtualHost configuration directs Apache requests to the Laravel application's `public` directory.

The default Apache site is disabled to prevent conflicts with the default VirtualHost configuration.

The `AllowOverride All` directive allows Laravel's `.htaccess` configuration to be processed, while `Require all granted` allows clients to access the application directory.

## Configure Firewall

The server firewall is configured using UFW (Uncomplicated Firewall) to control network access to the VPS.

Only ports required by the service are opened, while other unneeded ports are closed.

### Firewall Rules 

The following are the firewall rules used in deployment : 

```
| Port | Service | Access |
|------|---------|--------|
| 22 | SSH | Allowed |
| 80 | HTTP | Allowed |
| 443 | HTTPS | Allowed |
| 3306 | MySQL | Denied |
| 21 | FTP | Denied |
| 25 | SMTP | Denied |
```

### Firewall Verification

The firewall rules that have been implemented are then verified for their status to ensure the configuration is running correctly.

```bash
sudo ufw status
```

## Validate Application

Once the server and application configuration is complete, the Laravel application is validated to ensure the deployment is functioning correctly.

This validation focuses on application accessibility, database connectivity, and core application functionality.

### Application Accessibillity

The Laravel website is accessed through a web server domain previously configured on an Apache virtual host.

A successful response from the Laravel application confirms that Apache is correctly serving the application from the configured virtual host.

### Database Connectivity

Application database connectivity has been verified through the deployed Laravel application.

A successful connection confirms that the database configuration in the `.env` file and the MySQL server are functioning correctly.

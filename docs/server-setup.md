# Server Setup

## Operating System

---

Ubuntu Server 22.04 LTS

---
## Overview

This document describes the server environment built to host a futsal field booking website based on the Laravel framework.

The server is configured using the Ubuntu Server 22.04 LTS operating system running on a VPS as the web hosting method.

```

## Installed Components

|Component | Version |
| ........ | ....... |
| Ubuntu | 22.04 LTS |
| Apache | 2.4.58 |
| PHP | 8.3.6 |
| Laravel | 12.20.0 |
| MySQL | 8.0.45 |
| Composser | 2.7.1 |
| Git | 2.43.0 |
| OpenSSH Server | 3.0.13 | 
| ufw Firewall | 0.36.2 |

```

## Server Directory Layout

```text
/var/www/project.futsal/
├── app
├── artisan
├── bootstrap
├── composer.json
├── composer.lock
├── config
├── database
├── package.json
├── package-lock.json
├── phpunit.xml
├── public
├── resources
├── routes
├── storage
├── tests
├── vendor
└── vite.config.js
```
## Installed Services

Below are the services that are installed and configured on the server.

```
| Service | Purpose |
| ....... | ....... |
| Apache2 | Web Server |
| MySQL | Database Server |
| OpenSSH Server | Remote Administration |
| UFW Firewall | Network Security System |
```

## Apache VirtualHost

Laravel web booking will be displayed through apache virtualhost configuration.

```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/project.futsal/public

    <Directory /var/www/project.futsal>
        AllowOverride All
        Require all granted
    </Directory>
```

From the configuration display, it shows that the location of the Laravel web application is in the "public" directory.

## PHP Extensions

Below is a list of installed PHP extensions that are generally required for Laravel to run applications.

- bcmath
- ctype
- curl
- dom
- fileinfo
- gd
- intl
- json
- mbstring
- openssl
- PDO
- pdo_mysql
- tokenizer
- xml
- zip
- Zend OPcache

## Environment Configuration

Important application configuration data is stored in a single file called ".env".

- Application environment
- Application URL
- Database connection
- Cache configuration
- Mail configuration

This file is important because it contains credential information such as database password, database user, mail configuration and other credential information.

## Deployment Goal

The server environment was prepared to host a Laravel-based booking system with Apache as the web server and MySQL as the database backend.

The overall goal of this project is to build a server environment capable of running a futsal field booking system that is cheap, stable, and easy to maintain and upgrade in the future.

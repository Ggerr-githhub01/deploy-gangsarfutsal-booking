# Server Setup

## Overview

This document describes the initial server preparation before deploying the Laravel booking futsal application.
The publication target is an Ubuntu Server 22.04 VPS configured as a production web server.

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


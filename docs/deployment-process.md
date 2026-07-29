# Deployment Process

## Overview

This section of the document will explain the process of deploying a futsal booking website to an Ubuntu server.

The deployment was performed on a Virtual Private Server using Apache2 as the web server, PHP 8.2 as the runtime environment, and MySQL as the database server. The goal was to provide a stable production environment accessible through the public domain.

## Deployment Workflow

```text
Project Preparation
        │
        ▼
Upload Project via SCP
        │
        ▼
Verify Project Files
        │
        ▼
Install Application Dependencies
        │
        ▼
Configure Environment
        │
        ▼
Generate Application Key
        │
        ▼
Database Migration
        │
        ▼
Configure Apache VirtualHost
        │
        ▼
Configure File Permissions
        │
        ▼
Configure Firewall
        │
        ▼
Configure Domain
        │
        ▼
Deployment Validation

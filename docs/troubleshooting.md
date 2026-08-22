# Troubleshooting

## Overview

This document will describe the challenges and issues encountered during the development process.

Due to the considerable gap between the project's completion and this GitHub documentation, concrete evidence such as executed command results or system error displays may be incomplete. However, the issues documented here are real, not fabricated case studies.

## PHP & Composer Issue

The first problem topic discussed in this section is PHP & Composer Problems.

### PHP Version Mismatch with Composer

**Symptom**

Composer reports that the PHP version running on the command line does not match the PHP version required in ```composer.json```.

The development environment uses PHP 8.5.2, while the project's dependency requirements are incompatible with this PHP version.

**Cause**

The PHP version used in the development environment does not match the PHP version requirements needed by the project dependencies.

**Resolution**

Match the active PHP version on the production server command line to the version required in ```composer.json```.

**Result**

The PHP environment becomes compatible with the project's dependency requirements, so the Laravel deployment process can continue.

## Laravel Application Issues

### Artisan Command Error

**Symptom**

The Artisan command returns:

`Cannot open input file: artisan`

The command could not be executed by the PHP CLI.

**Cause**

php artisan command is executed in the wrong directory, that is, not in the main folder of the Laravel project which has the artisan file.

The error indicates that the `artisan` file is missing from the path where the command was executed.

**Resolution**

Before running the `artisan` command, make sure you're in the directory where your Laravel project is stored.

Then, make sure the `artisan` file is located in that directory.

**Result**

The `artisan` command can be executed properly after ensuring that it is in the directory file.

### Environment Configuration

**Symptom**

After the Laravel application environment is changed from development to production mode, the admin panel behavior changes.

The application configuration uses `APP_ENV=production` and `APP_DEBUG=false` as part of the production deployment configuration.

**Cause**

An application's behavior at runtime is influenced by its environment configuration. Changing `APP_ENV` and `APP_DEBUG` from development to production mode changes how Laravel handles application errors and its behavior at runtime.

**Resolution**

Laravel's `.env` configuration is reviewed and adjusted to ensure the application environment meets the desired deployment conditions.

The production configuration is maintained by:

```env
APP_ENV=production
APP_DEBUG=false
```

**Result**

The application can continue to run under its intended production configuration, with debug output disabled for the deployed environment.

## Apache Configuration Issues

### VirtualHost Configuration

**Symptom**

The Laravel application requires Apache to serve the application from Laravel's `public` directory, not from the project root directory.

**Cause**

The Apache VirtualHost configuration requires using the Laravel application's `public` directory as the web-accessible document root. Laravel's entry point is located at `public/index.php`, so presenting the project root does not provide the intended application entry point.

**Resolution**

The Apache VirtualHost configuration was reviewed and updated to use:

```apache
DocumentRoot /var/www/direktory-project/public
```

**Result**

Apache serves the Laravel application through the correct public directory, allowing the application to be accessed through the configured domain. The HTTPS/SSL configuration is then applied to the Apache deployment.

## Ubuntu Server Issues

### Hostname Resolution

**Symptom**

Administrative commands using `sudo` returned the following warning:

```text
sudo: unable to resolve host ukktkj11.web.id
```

The warning indicated that the server hostname could not be resolved correctly by the local system configuration.

**Cause**

The server hostname configuration was not correctly mapped in the local /etc/hosts configuration.

**Resolution**

The /etc/hosts configuration was reviewed and corrected so that the configured hostname could be resolved locally by the server.

**Result**

The hostname resolution issue was resolved, and the sudo warning no longer appeared during server administration.

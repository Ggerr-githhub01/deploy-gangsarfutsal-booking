# Troubleshooting

## Overview

This document will describe the challenges and issues encountered during the development process.

Due to the considerable gap between the project's completion and this GitHub documentation, concrete evidence such as executed command results or system error displays may be incomplete. However, the issues documented here are real, not fabricated case studies.

## PHP & Composer Issue

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

The Artisan command returns:

`Cannot open input file: artisan`

The command could not be executed by the PHP CLI.

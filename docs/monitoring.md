# Monitoring Server

## Overview

After the web server project has been successfully implemented to completion, the next process is to monitor the server performance while the system is running.

This server monitoring process is conducted separately from the deployment process. Using additional tools such as Kuma Uptime, the Gangsar Futsal project is the primary target of this server monitoring process.

## Monitoring Scope

Monitoring activities are focused on service availability and connectivity using Kuma Uptime.

The monitored ascpets included: 

- **Availabillity** - Monitors whether configured targets are reachable and operational.
- **Uptime** - records the percentage of time the target was considered “Up” during the period shown.
- **Response Time** - measures how long it takes the target to respond to a monitoring check.
- **Service Status** - Monitor the availability of selected services and endpoints, including MySQL, Apache, and other configured targets.


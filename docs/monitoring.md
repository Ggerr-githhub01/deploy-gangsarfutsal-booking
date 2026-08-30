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

## Monitoring Architecture

The monitoring architecture describes the relationship between the monitored services, Kuma Uptime, and the monitoring results collected during monitoring activities.

![Monitoring Architecture](../diagrams/diagram%20monitoring%20server.drawio.png)

## Monitoring Tools

The server environment used will be continuously monitored to ensure the system remains optimal.

In this situation, technicians use Kuma Uptime as the primary tool in the server performance monitoring process.

### Uptime Kuma

Uptime Kuma was used as the primary monitoring tool to monitor the availability and status of configured services and endpoints.

The monitoring dashboard provided information including:

- Service availabillity status
- Uptime percentage
- Response time
- Ping latency
- Up/Down status history
- Connection failure events

## Metrics Monitored

In the process of monitoring server performance using Kuma Uptime, monitoring only focuses on service availability and connectivity.

Monitored metrics and status information include:

### Availabillity Status

The service availability status in Kuma's uptime monitoring process is identified using the terms "Active" and "Inactive" which indicate the availability of the monitoring target.

### Uptime precentage

Kuma Uptime records the percentage of availability of monitored targets over various time periods, including 24 hours, 30 days, and 1 year, etc.

### Response time 

Response times are monitored in milliseconds to observe the target's response latency.

The dashboard typically displays the average response latency over time and the lowest response latency the target has ever sent.

## Monitoring Configuration

Uptime Kuma is configured to monitor multiple servers simultaneously, as well as to observe how the system performs after deployment.

### Monitor Targets

Kuma Uptime is targeted to monitor the performance of services running on a server environment, as well as notify you if there are any problems with it at any time.

The configured targets included Apache, MySQL, web endpoints, and external network targets.

### Monitor types

Several types of monitors are configured according to the type of target being monitored.

For the MySQL service, Uptime Kuma used TCP Port monitoring with the following target:

- Host: `localhost`
- Port: `3306`

### Monitoring Parameters

Each monitor is configured with parameters appropriate to its target. This configuration includes the target address and the monitoring method needed to determine service availability.

The monitoring dashboard records availability status, response time, and the resulting status history.

## Monnitoring Results

Server environmental conditions will be continuously monitored to maintain stable performance.

All monitoring results will be displayed in real time via the monitoring dashboard.

### Service Availabillity

The monitoring dashboard displays the availability of the targeted configuration service.

This is indicated by the statement "Up," meaning the service is available, and "Down," meaning the service is unavailable.

### Uptime & Response Time

Uptime Kuma provides statistical information in the form of response times for monitored targets.

Response time is measured in milliseconds and reflects how quickly the target responds to monitoring, along with the average response time over a specified period.

For example, the captured monitoring data shows an uptime of 96.03%, with a current ping of 1 ms and an average ping of 1.24 ms over the displayed period.

![Server Availabillity](../screenshoots/monitoring%20server.jpg)

### Status History

Uptime Kuma records every change that occurs to the monitored target and displays it on the dashboard in real time.

Stored monitoring logs indicate when the target has experienced a loss of service availability, indicated by the Up and Down statuses on the monitoring dashboard.

This historical information provides a baseline record of service availability incidents during the monitoring period.

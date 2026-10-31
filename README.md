# Windows Login Failure Detection and Investigation Using Splunk

## Project Overview

This project demonstrates how a Security Operations Center (SOC) analyst can use Splunk to detect and investigate failed Windows login attempts.

The project focuses on analysing Windows Security Event Logs, identifying repeated authentication failures, investigating suspicious login patterns, and developing security monitoring queries using Splunk Search Processing Language (SPL).

## Objectives

- Understand Windows authentication events.
- Identify failed login attempts using Windows Event ID 4625.
- Detect repeated login failures within a defined time window.
- Investigate usernames, source IP addresses, and event timestamps.
- Develop SPL queries for security monitoring.
- Create a dashboard and configure detection alerts.
- Document investigation findings and recommended responses.

## Tools and Technologies

- Splunk Enterprise
- Windows Security Event Logs
- Splunk Search Processing Language (SPL)
- GitHub

## Project Status

Completed

## Data and Testing

Initial testing will use simulated or test Windows security events. Detection results will be validated against the available data.

Simulated events will be clearly identified and will not be represented as real security incidents.

## Expected Deliverables

- Windows login failure event samples
- SPL detection queries
- Investigation notes
- Security monitoring dashboard
- Alert configuration
- Sample incident report
- Screenshots of project testing

## Disclaimer

This project is intended for educational and portfolio purposes. It does not represent professional SOC employment experience.

Project Screenshots

The following screenshots demonstrate the searches performed in Splunk using synthetic Windows authentication events.

1. Windows Event Ingestion

2. Failed Login Detection

3. Potential Brute-Force Activity

4. Failed Logins and Successful Authentication

## Detection Scenarios

### 1. Windows Failed Login Detection
- Event ID: 4625
- Identified failed login attempts by account and source IP address.
- Counted authentication failures to identify accounts requiring further investigation.

### 2. Potential Brute-Force Activity
- Aggregated failed login attempts by source IP.
- Applied a threshold of three or more failed attempts.
- Identified IP addresses associated with repeated authentication failures.

### 3. Failed Logins Across Multiple Accounts
- Identified source IP addresses associated with failed login attempts against three or more distinct accounts.
- Reviewed targeted account names to identify suspicious authentication patterns.

### 4. Failed Logins Followed by Successful Authentication
- Analyzed failed login (Event ID 4625) and successful login (Event ID 4624) events.
- Identified account and source IP combinations containing both event types.
- Flagged the pattern for further investigation rather than treating it as confirmed account compromise.

## Tools and Skills Demonstrated

- Splunk Enterprise
- Search Processing Language (SPL)
- Windows authentication event analysis
- Security event aggregation and filtering
- Source IP and account investigation
- Basic detection logic development
- Incident documentation

## Dataset Disclaimer

This project uses synthetic Windows authentication events created for educational purposes. The results demonstrate detection logic and investigation techniques; they do not represent a confirmed real-world security incident.

### Windows Authentication Monitoring Dashboard

Created a Splunk dashboard to visualize and investigate simulated Windows authentication events.

Dashboard panels:
- Windows Authentication Events by Event ID
- Failed Login Attempts by User and Source IP
- Potential Brute-Force Login Activity by Source IP
- Failed and Successful Logins by User and Source IP

Skills demonstrated:
- SPL query development
- Windows authentication event analysis
- Failed login investigation
- Suspicious authentication pattern detection
- Security dashboard creation and visualization

Note: This project uses simulated Windows security event data for educational and demonstration purposes.

5. Multiple Accounts Targeted by One IP

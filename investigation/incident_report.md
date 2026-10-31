# Windows Login Failure Investigation Report

## 1. Project Overview

Project: Windows Login Failure Detection and Investigation Using Splunk SIEM  
Data Source: Synthetic Windows security event CSV  
Tool: Splunk Enterprise  
Investigation Type: Authentication event analysis

## 2. Objective

To analyze Windows authentication events, identify repeated failed login attempts, identify source IP addresses associated with suspicious activity, and investigate failed logins followed by successful authentication.

## 3. Events Analyzed

| Event ID | Description | Events Observed |
|---|---|---:|
| 4624 | Successful logon | 1 |
| 4625 | Failed logon | 8 |
| 4740 | Account locked out | 1 |

## 4. Findings

### Finding 1: Repeated Failed Login Attempts

- Account: jsmith
- Source IP: 192.168.1.25
- Failed attempts: 5

Five failed login attempts were observed for the same account and source IP. This pattern may indicate repeated password guessing and warrants further investigation.

### Finding 2: Failed Logins Across Multiple Accounts

- Source IP: 192.168.1.50
- Failed attempts: 3
- Accounts: admin, administrator, testuser

Three failed login attempts targeted different accounts from the same IP address. This pattern may indicate password guessing across multiple accounts.

### Finding 3: Failed Logins Followed by Successful Authentication

- Account: jsmith
- Source IP: 192.168.1.25
- Failed attempts: 5
- Successful attempts: 1

The dataset contains failed login attempts followed by a successful login for the same account and IP address. This sequence warrants investigation, but it does not independently establish that an account was compromised.

## 5. Recommended Investigation Steps

1. Validate the activity against the original Windows security logs.
2. Check whether the source IP belongs to an authorized user or system.
3. Review authentication timestamps and surrounding security events.
4. Check for other suspicious activity associated with the account.
5. Escalate if evidence supports suspected account compromise.

## 6. Conclusion

Splunk searches were used to count authentication events, identify repeated failures, examine failures across multiple accounts, and correlate failed and successful login events.

Note: This project uses synthetic sample data for educational and portfolio purposes. The findings are simulated and do not represent a confirmed real-world security incident.

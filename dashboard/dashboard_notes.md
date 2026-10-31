# Windows Authentication Monitoring Dashboard

## 1. Overview

This document describes the planned dashboard for the Windows Login Failure Detection and Investigation project using Splunk SIEM.

The dashboard is intended to summarize Windows authentication activity and help identify suspicious login patterns in a synthetic dataset.

## 2. Tools Used

- Splunk Enterprise
- Search Processing Language (SPL)
- Synthetic Windows authentication event data

## 3. Dashboard Panels

### Panel 1: Windows Authentication Events

**Objective:** Display the number of events by Windows Event ID.

```spl
index=main
| stats count by EventCode
| sort EventCode
```

Expected event IDs:
- 4624 — Successful logon
- 4625 — Failed logon
- 4740 — Account locked out

### Panel 2: Failed Login Attempts by Account

**Objective:** Identify accounts with repeated failed login attempts.

```spl
index=main EventCode=4625
| stats count AS failed_attempts by Account_Name
| sort - failed_attempts
```

### Panel 3: Failed Login Attempts by Source IP

**Objective:** Identify source IP addresses associated with repeated authentication failures.

```spl
index=main EventCode=4625
| stats count AS failed_attempts by Source_IP
| sort - failed_attempts
```

### Panel 4: Multiple Accounts Targeted by One IP

**Objective:** Identify source IP addresses associated with failed login attempts against three or more distinct accounts.

```spl
index=main EventCode=4625
| stats count AS failed_attempts
    dc(Account_Name) AS unique_accounts
    values(Account_Name) AS targeted_accounts
    by Source_IP
| where unique_accounts >= 3
| sort - unique_accounts
```

### Panel 5: Authentication Activity Over Time

**Objective:** Visualize authentication events over time to help identify periods of increased activity.

```spl
index=main (EventCode=4624 OR EventCode=4625)
| timechart span=1m count by EventCode
```

**Note:** Verify that Splunk has correctly interpreted the event timestamps before relying on this panel. If necessary, configure timestamp extraction for the CSV source type.

## 4. Investigation Use Cases

The dashboard is intended to support:

- Monitoring successful and failed authentication events.
- Identifying accounts with repeated login failures.
- Investigating source IP addresses associated with suspicious activity.
- Identifying failed logins targeting multiple accounts.
- Reviewing authentication activity over time.

## 5. Limitations

- The dataset contains synthetic events created for educational purposes.
- Detection thresholds are examples and may require tuning in a real environment.
- Repeated failures do not independently confirm a brute-force attack.
- Dashboard panels require validation against the actual indexed data.

## 6. Future Improvements

- Build and save an interactive Splunk dashboard using these searches.
- Add time-based correlation for failed logins followed by successful authentication.
- Add appropriate visualizations and time-range controls.
- Document dashboard results with screenshots.

## 7. Project Disclaimer

This project demonstrates hands-on SIEM searching and authentication analysis in a learning environment. It does not represent a confirmed real-world security incident.

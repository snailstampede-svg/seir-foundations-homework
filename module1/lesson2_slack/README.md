# Lesson 2 Homework: Slack Alerts from EC2

**Date:** 11-5-2026
**Environment:** EC2 instance (`ec2-user@ip-172-31-22-137`), project folder `/opt/balerica-bank`, Python venv
**Channel:** `#balerica-alerts`

## Overview

This week I ran seven small Python scripts that each send a message to Slack through the `send_alert(agent, severity, message, incident_id)` function in `slack.py`. The scripts progress from a simple hello message to a monitoring report that combines disk, CPU, and time checks. Behavior is controlled by two settings in `.env`:

| Setting | Purpose |
|---|---|
| `SLACK_ALERT_SEVERITY` | Minimum severity that gets sent (INFO, WARNING, ERROR, CRITICAL) |
| `SLACK_ALERTS_ENABLED` | Kill switch: `true` sends alerts, `false` skips all of them |

## Setup

1. Pulled the course repo and copied `hw*.py` into `/opt/balerica-bank/` next to `slack.py`.
2. Set `SLACK_ALERT_SEVERITY=INFO` in `.env` so the INFO-level homework alerts would be delivered.
3. Activated the venv with `source venv/bin/activate`.

## Script Notes

### 1. `hw1_hello_slack.py`: Hello Slack
The script sends whatever is in the message field. I edited `MY_NAME` to use my own name, but I could edit the script to send any message I needed to relay.

### 2. `hw2_severity_tour.py`: Severity Tour
The script loops through all four severities (`INFO`, `WARNING`, `ERROR`, `CRITICAL`). With `SLACK_ALERT_SEVERITY=INFO`, every message is forwarded, since INFO is the lowest level and the threshold passes that level and everything above it. With `SLACK_ALERT_SEVERITY=ERROR`, only 2 messages arrived (ERROR and CRITICAL), because `.env` filters out everything below the configured level.

### 3. `hw3_server_time.py`: Server Time
Servers use UTC because it is universal and unambiguous. It has no Daylight Saving shifts, and it is a fixed reference based on atomic clocks (maintained by the BIPM from roughly 450 clocks worldwide), so no local offset can change it. That makes it the common denominator for distributed systems.

My local clock read 2:01 PM PST while UTC read 22:01, an 8-hour difference.

### 4. `hw4_disk_watch.py`: Disk Watch
The script measures disk usage and picks a severity with if/else logic:

```python
if percent_used >= 90:
    severity = "ERROR"
elif percent_used >= 75:
    severity = "WARNING"
else:
    severity = "INFO"
```

- 90% or more: `ERROR`
- 75% or more: `WARNING`
- Otherwise: `INFO`

**Why a quiet INFO is good design:** useless alerts are noise. You don't want to be alerted when things are fine, only when something is wrong.

### 5. `hw5_load_check.py`: Load Check
The script reads the CPU load average over the last 1, 5, and 15 minutes. It sets the severity to `WARNING` if the 5-minute average is greater than the CPU count, meaning the server is busy. This could happen if Balerica Bank were flooded with requests or under attack.

### 6. `hw6_incident_drill.py`: Incident Drill
The script generates a random (fake) incident with varying severity levels. In my view, only `CRITICAL` is serious enough to wake someone at 3 AM. The lower levels could be traffic spikes that resolve on their own.

### 7. `hw7_morning_report.py`: Morning Report
The hw7_morning_report.py script, provides a generic informational report regarding the date/time, server details includeing disk usage, CPU load and overall status as shown below:

- Time: 2026-11-05 23:05:28 UTC
- Host: ip-172-31-22-137.ec2.internal (Linux x86_64)
- Python: 3.9.25
- Disk on / : 25.6% used
- Load (1m): 0.00
- Status: all checks ran. The bank greets the day.

## Experiments

### Experiment 1: Threshold set to CRITICAL
- **Setting:** `SLACK_ALERT_SEVERITY=CRITICAL`, then reran `hw2_severity_tour.py`
- **Prediction:** only one message (CRITICAL) would arrive.
- **Result:** only the CRITICAL message was delivered, which matched my prediction (see screenshot).

### Experiment 2: Kill switch
With `SLACK_ALERTS_ENABLED=false`, the script ran but no messages were delivered. Everything was skipped:

```text
(venv) [ec2-user@ip-172-31-22-137 balerica-bank]$ python hw1_hello_slack.py
Skipped. Check .env: SLACK_ALERTS_ENABLED must be true and SLACK_ALERT_SEVERITY=INFO (see homework README).
```
While conducting maintenance, it is advisable to activate the kill switch for alerts.  The kill switch keeps the channel clean so a genuine alert is not buried in noise, prevents spamming false alarms/alerts that would essential page people unnecessarily. Once the maintenance window is completed, the switch can be returned to true allowing normal alert messaging.

### Experiment 3: Lowering the disk WARNING threshold
I lowered the WARNING threshold in `hw4_disk_watch.py` from 75 to 20, below my current usage:

```python
if percent_used >= 90:
    severity = "ERROR"
elif percent_used >= 20:
    severity = "WARNING"
```

On rerun the severity changed to `WARNING`:

```text
(venv) [ec2-user@ip-172-31-22-137 balerica-bank]$ python hw4_disk_watch.py
Disk is 25.6% used -> severity WARNING.
Skipped by threshold — that can be correct behavior!
```

The message was skipped because the `.env` threshold was still above WARNING at that point, which shows the severity logic and the delivery filter are separate.

### Experiment 4: Restore settings
All settings were returned to normal:

```dotenv
SLACK_ALERTS_ENABLED=true
SLACK_ALERT_SEVERITY=INFO
```

## Evidence

- **Slack screenshot (five or more homework alerts):** `screenshots/slack_alerts.png` *(update path)*
- **Terminal screenshot (`hw7_morning_report.py` with Lesson 1 ID line):** `screenshots/hw7_morning_report.png` *(update path)*

## Rules Followed

- Only synthetic messages were sent. No passwords, keys, customer data, or `.env` contents went to Slack.
- Each script sent only a handful of messages, with no loops firing alerts repeatedly.
- `send_alert(agent, severity, message, incident_id)` was left unchanged.

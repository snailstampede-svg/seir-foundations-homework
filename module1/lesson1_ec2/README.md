# SEIR Foundations — Module 1, Lesson 1 Homework

**Student Name:** \Ernie

**Course:** SEIR Foundations

**Lesson:** Module 1 / Lesson 1 — EC2 + Balerica Legacy Bank

**Deadline:** Tuesday, November 3, 2026, at 12:00 PM Central Time

## 1. Lab Execution Tracking (7 Runs)

Per the assignment guidelines, the lab was executed seven (7) times across separate fresh EC2 instances. Every run includes the mandatory ID line (`whoami && TZ='America/Los_Angeles' date && ec2-metadata -i && uptime -s`) prior to starting the FastAPI server.

> **Daily Screenshot Limit Compliance:** No more than 3 runs were executed on any single calendar date, ensuring adherence to the multi-day requirement.

### Evidence Table

| run | date       | time_zone | instance_id         |      boot_time      | public_ipv4_dns | screenshot                | terminated |
|-----|------------|-----------|---------------------|:-------------------:|-----------------|---------------------------|------------|
| 1   | 10/29/2026 | PDT       | i-0b30ab9be43fe9d79 | 2026-10-30 03:32:33 | 52.90.70.20     | screenshots/lab1_run1.jpg | yes        |
| 2   | 10/29/2026 | PDT       | i-0f129db6bdfd4848a | 2026-10-30 04:12:08 | 54.89.99.180    | screenshots/lab1_run2.jpg | yes        |
| 3   | 10/29/2026 | PDT       | i-04af93847a735d87f | 2026-10-30 04:51:41 | 35.153.73.54    | screenshots/lab1_run3.jpg | yes        |
| 4   | 10/31/2026 | PDT       | i-0afee923e18bb4f26 | 2026-10-31 14:33:56 | 35.153.132.151  | screenshots/lab1_run4.jpg | yes        |
| 5   | 10/31/2026 | PDT       | i-0e69c6739fb88614e | 2026-10-31 14:53:34 | 3.85.220.24     | screenshots/lab1_run5.jpg | yes        |
| 6   | 10/31/2026 | PDT       | i-088ee9e2809b6903a | 2026-10-31 15:04:55 | 3.80.233.192    | screenshots/lab1_run6.jpg | yes        |
| 7   | 1/11/2026  | PST       | i-0410ebb00b9878fa5 | 2026-11-02 03:53:31 | 98.93.106.61    | screenshots/lab1_run7.jpg | yes        |

## 2. Environment Verification & Diagnostics

### ID Line Format Used

```
whoami && TZ='America/Los_Angeles' date && ec2-metadata -i && uptime -s

```
## 3. COBOL Core Return Codes Reference

| Code | Status Meaning | Trigger Scenario Tested |
| ----- | ----- | ----- |
| **0** | Success | Account found (`/cobol/bin/account_lookup 100001`) or valid payment posted |
| **4** | Warning | Account not found in ledger (`/cobol/bin/account_lookup 999999`) |
| **8** | Business Rejection | Invalid payment parameters (e.g., zero amount, inactive account, insufficient balance) |
| **12** | Environment Failure | Command executed outside required directory (`/opt/balerica-bank`) or missing ledger files |

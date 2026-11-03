# SEIR Foundations — Module 1, Lesson 1 Homework
**Student Name:** [Your Name Here]  
**Course:** SEIR Foundations  
**Lesson:** Module 1 / Lesson 1 — EC2 + Balerica Legacy Bank  
**Deadline:** Tuesday, November 3, 2026, at 12:00 PM Central Time  

---

## 1. Lab Execution Tracking (7 Runs)

Per the assignment guidelines, the lab was executed seven times across separate fresh EC2 instances. Every run includes the mandatory ID line (`whoami && TZ='[Your/Timezone]' date && ec2-metadata -i && uptime -s`) prior to starting the FastAPI server.

> **Daily Screenshot Limit Compliance:** No more than 3 runs were executed on any single calendar date, ensuring adherence to the multi-day requirement.

### Evidence Table

| Run | Date (local) | Time zone | Instance ID | Boot time (UTC) | Public IPv4 DNS | Screenshot | Terminated? |
|:---:|:------------:|:---------:|:-----------:|:---------------:|:---------------:|:----------:|:-----------:|
| 1 | YYYY-MM-DD | [Your Timezone] | i-xxxxxxxxxxxxxxxxx | YYYY-MM-DD HH:MM:SS | ec2-xx-xx-xx-xx.compute-1.amazonaws.com | `screenshots/lab1_run1.jpg` | Yes |
| 2 | YYYY-MM-DD | [Your Timezone] | i-xxxxxxxxxxxxxxxxx | YYYY-MM-DD HH:MM:SS | ec2-xx-xx-xx-xx.compute-1.amazonaws.com | `screenshots/lab1_run2.jpg` | Yes |
| 3 | YYYY-MM-DD | [Your Timezone] | i-xxxxxxxxxxxxxxxxx | YYYY-MM-DD HH:MM:SS | ec2-xx-xx-xx-xx.compute-1.amazonaws.com | `screenshots/lab1_run3.jpg` | Yes |
| 4 | YYYY-MM-DD | [Your Timezone] | i-xxxxxxxxxxxxxxxxx | YYYY-MM-DD HH:MM:SS | ec2-xx-xx-xx-xx.compute-1.amazonaws.com | `screenshots/lab1_run4.jpg` | Yes |
| 5 | YYYY-MM-DD | [Your Timezone] | i-xxxxxxxxxxxxxxxxx | YYYY-MM-DD HH:MM:SS | ec2-xx-xx-xx-xx.compute-1.amazonaws.com | `screenshots/lab1_run5.jpg` | Yes |
| 6 | YYYY-MM-DD | [Your Timezone] | i-xxxxxxxxxxxxxxxxx | YYYY-MM-DD HH:MM:SS | ec2-xx-xx-xx-xx.compute-1.amazonaws.com | `screenshots/lab1_run6.jpg` | Yes |
| 7 | YYYY-MM-DD | [Your Timezone] | i-xxxxxxxxxxxxxxxxx | YYYY-MM-DD HH:MM:SS | ec2-xx-xx-xx-xx.compute-1.amazonaws.com | `screenshots/lab1_run7.jpg` | Yes |

---

## 2. Environment Verification & Diagnostics

### ID Line Format Used
```bash
whoami && TZ='[Your/Timezone]' date && ec2-metadata -i && uptime -s
```

### System Architecture Overview
```text
SWIFT Traffic Generator        (swift/traffic_generator.py)
         |
         v  HTTP / JSON
      FastAPI                  (app/main.py)
         |
         v  subprocess
   cobol_bridge.py             (app/cobol_bridge.py)
         |
         v  argv + KEY=VALUE stdout
account_lookup / payment_post  (cobol/*.cob, compiled by GnuCOBOL)
         |
         v  fixed-width records
accounts.dat / payments.dat    (data/)
         |
         v  export / ingest
       SQLite                  (data/bank.db — system of record)
```

---

## 3. COBOL Core Return Codes Reference

| Code | Status Meaning | Trigger Scenario Tested |
|:----:|:---------------|:------------------------|
| **0** | Success | Account found (`/cobol/bin/account_lookup 100001`) or valid payment posted |
| **4** | Warning | Account not found in ledger (`/cobol/bin/account_lookup 999999`) |
| **8** | Business Rejection | Invalid payment parameters (e.g., zero amount, inactive account, insufficient balance) |
| **12** | Environment Failure | Command executed outside required directory (`/opt/balerica-bank`) or missing ledger files |

---

## 4. Extra Credit Progress (Be A Man - BAM)

| Module | Objective | Status | Artifact / Screenshot |
|:------:|:-----------|:------:|:---------------------:|
| **BAM 2.1** | Bedrock Integration (`/ask` using Claude) | [Completed / Incomplete] | `screenshots/BAM_2.1.jpg` |
| **BAM 2.2** | Baked Launch Template (User Data script) | [Completed / Incomplete] | `screenshots/BAM_2.2.jpg` |
| **BAM 2.3** | Golden AMI Creation and Deployment | [Completed / Incomplete] | `screenshots/BAM_2.3.jpg` |

---

## 5. Directory Verification Checklist

- [ ] All 7 lab run screenshots populated under `screenshots/`
- [ ] Quiz screenshots uploaded (`Maarek_Section21_quiz.jpg`, `23`, `25`)
- [ ] COBOL practice screenshots uploaded (`cobol_rc0.jpg` through `rc12.jpg`, `cobol_ledger_decode.jpg`)
- [ ] Git clone evidence uploaded (`git_clone.jpg`)
- [ ] `lab1_notes.md` updated with notes for all 7 runs and COBOL practice data
- [ ] `ai_review_[YourName].txt` and `spotter_[YourName].txt` completed
- [ ] `AI_enabled_study_lab1.0.txt` updated with 5-topic research write-ups
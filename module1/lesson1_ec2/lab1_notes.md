
# Lab1_notes

 These are the notes gathered for my lab1_ec2 Exercises

Step 1. Once connected to the instance, run the command to generate the ID line

whoami && TZ='America/Los_Angeles' date && ec2-metadata -i && uptime -s

This command returns the following output:

ec2-user
Thu Oct 29 20:39:18 PDT 2026
instance-id: i-0b30ab9be43fe9d79
2026-10-30 03:32:33

***CORRECTION: Per assignment instructions -  THIS COMMAND SHOULD BE RUN LATER IN THE LAB RIGHT BEFORE STARTING UVICORN.***

--------

- ## Run #1 InstanceID: i-0b30ab9be43fe9d79

    1. I neglected to perform the COBOL core practice exercises for run #1.
    2. I initially misunderstood the placement of the ID line for the assignment, but I caught my error before applying it to my assignment.

The following is a unique line for this instance:
INFO:     Started server process [36797]

This should only show up for this particular instance.

- Run #2
The following is a uniqe line for this instance:
INFO:     Started server process [36968]

- Run#3
At this point I realized that the unique marker for all my runs were captured in the screenshots. Once uvicorn is started, the server process number is posted to screen.

- Run #4
The following is a unique line for this instance:
INFO:     Started server process [35723]

- Run #5
Nothing of note occurred during this run.
- Run #6

The following is a unique line for this instance:
INFO:     Started server process [35895]

I performed the COBOL core practice on this run.



## COBOL Practice

- Lab run #6
- Instance ID -i-088ee9e2809b6903a

Command run: ./cobol/bin/account_lookup 100001

Output:
ACCOUNT=100001
NAME=Alice Johnson
STATUS=ACTIVE
BALANCE=5000.00
CURRENCY=USD

Code: 0 Success

Command Run: ./cobol/bin/account_lookup 999999

Output:
ERROR=ACCOUNT NOT FOUND
ACCOUNT=999999

4 — account not found

Command Run: ./cobol/bin/payment_post TXN-XX-0001 100001 0.00 USD TEST-ZERO

output:
TXN=TXN-XX-0001
ACCOUNT=100001
AMOUNT=0.00
CURRENCY=USD
STATUS=REJECTED
REASON=AMOUNT MUST BE GREATER THAN ZERO


Command run: (this was run from the wrong folder) /opt/balerica-bank/cobol/bin/account_lookup 100001

output:

ERROR=CANNOT OPEN data/accounts.dat
FILE-STATUS=35
-------


sqlite is installed on the system. The bank keeps a table called "accounts" nad one called "transactions" as shown by the output below:

[ec2-user@ip-172-31-36-241 balerica-bank]$ sqlite3 data/bank.db ".tables"
accounts      transactions
[ec2-user@ip-172-31-36-241 balerica-bank]$ sqlite3 data/bank.db ".schema"
CREATE TABLE accounts (
    account_id TEXT PRIMARY KEY,
    customer_name TEXT NOT NULL,
    status TEXT NOT NULL,
    balance REAL NOT NULL,
    currency TEXT NOT NULL
);
CREATE TABLE transactions (
    transaction_id TEXT PRIMARY KEY,
    account_id TEXT NOT NULL,
    amount REAL NOT NULL,
    currency TEXT NOT NULL,
    status TEXT NOT NULL,
    reference TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

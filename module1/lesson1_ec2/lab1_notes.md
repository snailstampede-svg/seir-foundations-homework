
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
I performed the COBOL core practice on this run.

## COBOL Practice

- Lab run #6
- Instance ID -i-088ee9e2809b6903a
    1. `./cobol/bin/payment_post EM-0001 100001 125.50 USD INV-1001` - This command successfully posts a payment and returns the success code `0`

    2. `./cobol/bin/account_lookup 123456` this command searches for account#999999. Since there is no account with that number, we get an error code `4`
    3. `./cobol/bin/payment_post EM-0001 100001 000.00 123 INV-1002` This command attempts to post a payment with a value of '0' which is rejected with the error code `8`
    4. I could not figure out how to generate a return code 12.

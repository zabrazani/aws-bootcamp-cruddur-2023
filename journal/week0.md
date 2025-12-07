# Week 0 — Billing and Architecture

## Required Homeworks/Tasks

### Install AWS CLI FOR ONA LINUX

I was able to use ONA (formally known as gitpod) to install using the terminal and use AWS CLI.

I did  the following steps to install AWS CLI.

I installed theAWS CLI via command in **ONA CODE TERMINAL**:
I followed the Intructions on the [AWS CLI Install Documentation Page](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)


![Installing AWS CLI](assets/installing-AWS-CLI-ONA.png)

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```


###Install anf Verify AWS CLI FOR WINDOWS 10 OR 11

Providing Instructions I used for my configuration on my local machine on windows.
I did the following instructions to install my AWS CLI

I Installed the following AWS CLI for windows command in **Command Prompt**:

I followed the instructions on the [AWS CLI Install Documentaton Page](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) 

```
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```
After the Installion, I closed my command prompt and opened it again and it worked Prove with screenshoot below 
![VERIFYING AWS CLI](assets/aws%20cli%20windows.png)


###Creating a Budget
I created my own Budget for $1 per dollar for each Budgets because I cannot afford any kind of spend.
I did not create a third Budget because creating a third budget spendig goes over my free limit and AWS will charge me.

![Image of the Budget Alarm I Created](assets/Budget-alarm.png)

### Recreate Logical Archetecture Design in Lucid Charts

![Cruddur Logical Design](assets/Logical-Arctechiture-Diagram.png)
## Homework Challenge 

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

![Cruddur Logical Design](assets/Cruddur%20logical%20Diagram.png)

[Lucid Chart Shared Links](https://lucid.app/lucidchart/5564adc0-83b5-4b8f-9361-5c187c1f0f2e/edit?invitationId=inv_d0c43cbb-17f3-49a0-aaa3-a1f12f033db1)

## Homework Challenge 

### Adding Security Components to the Logical Diagram

I added AWS Web Application Firewall (AWS WAF) to my Diagram to enhance web security.

Firtly I have to define a AWS WAF  
AWS WAF (Web Application Firewall) is a cloud-based security service that protects web applications and APIs from common exploits and bots by filtering and monitoring HTTP/HTTPS traffic based on customizable rules, allowing you to allow, block, or count requests matching conditions like IP addresses, SQL injection, or cross-site scripting. It integrates with AWS resources like CloudFront, API Gateway, and Application Load Balancers to enforce security policies at the edge. 

Protection: WAF rules can help block SQL injection, cross-site scripting (XSS), and known malicious IP addresses.

I Placed an AWS WAF in front of your Load Balancer. This protects your application from common web exploits and bots that could affect availability, compromise security, or consume excessive resources.

![Cruddur Logical Design With Added Security](assets/Cruddur%20logical%20Diagram%20(1).png)
[Lucid chart shared links](https://lucid.app/lucidchart/5564adc0-83b5-4b8f-9361-5c187c1f0f2e/edit?invitationId=inv_d0c43cbb-17f3-49a0-aaa3-a1f12f033db1)

### Referencing AWS WAF
[Google](https://www.google.com/search?q=define+aws+waf&oq=define+aws+awf&gs_lcrp=EgZjaHJvbWUqCAgBEAAYDRgeMgYIABBFGDkyCAgBEAAYDRgeMg0IAhAAGIYDGIAEGIoFMg0IAxAAGIYDGIAEGIoFMg0IBBAAGIYDGIAEGIoFMgoIBRAAGIAEGKIEMgoIBhAAGIAEGKIEMgoIBxAAGIAEGKIEMgcICBAAGO8F0gEJMTM5MzVqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8)

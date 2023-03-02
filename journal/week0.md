# Week 0 — Billing and Architecture

# Preparation

Create a Github Account. You will copy Andrew's repository with the right formatting of the repo and must be public.
Create a Gitpod account and install the extension for your browser.
Create Github CodeSpace.
Create the AWS account (This is the important one as you will spin all the services here). Make sure you have a credit/debit card ready.
Create Lucidchart. This app allows you to create chart/diagrams. Having a visual structure is useful to see the overview of what are you creating.
Create Honeycomb.io account.
Create Rollbar account.

Billing Alerts
There are 2 ways to set the billing alerts.

Using Budget.
Using Cloudwatch Alarm. In this case, you need to create an alarm on us-east-1 region (since it is the only region you can create an alarm). You can create up to 10 free cloudwatch alarm
Those 2 alarms will be helpful to identify if you are underspending/overspending.

Free Tier
This section will show all the usage of your free tier. It will show all the services free for the 12 months (starting with the registration) and their usage and forecast. After 12 months, they are still some services that are always free. And also there is some service that is "Trial" which means that is available for a short period such as 30 days.

Tags
Tags (are Key/Value pair) are useful when you want to know how your cost is allocated. For example, if your want to identify all the services you used under the tag environment: dev (for example)

Cost Explorer
Cost explorer is a service which visualises, understands and manages your AWS costs usage over time.

Report
The section report allows for generating reports. there are some reports already created by AWS that you can use

Credit
This is the section where you submit the credit that you have to obtain during an event (for example after submitting a feedback questionnaire). And also it shows when the expiration date.

AWS Calculator
This is a tool where you want to estimate the cost of one or more services. Useful when someone asks you to give an estimated cost of the service you are going to use. I used this tool during some exercises on skillbuilder.

https://calculator.aws/#/




# Architecture Diagram

Logical Diagram - https://lucid.app/lucidchart/30f63eaa-cb19-4410-bccb-e3adf02a675d/edit?invitationId=inv_45d1e5d2-973d-45ec-8eb5-f24c4d2248c6


![Cruddur Logical Diagram](https://user-images.githubusercontent.com/70094537/222438504-b51e05a3-ac92-4a20-980b-ae9b51fb870f.png)

Conceptual Diagram - https://lucid.app/lucidchart/8a29c6e0-6edb-4da9-8227-f6714c1302da/edit?invitationId=inv_a4b72c96-798f-408e-95a3-96e6e77bc436

![Cruddur Conceptual Diagram](https://user-images.githubusercontent.com/70094537/222438933-36508bf1-f930-48a3-9603-1094598607e2.png)

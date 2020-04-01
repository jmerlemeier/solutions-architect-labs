#Procedure for AWS IAM 

## Overview
1. Access AWS through AWS Console in browser, AWS SDK, or AWS CLI.
2. Navigate to IAM service and notice the 'region' is 'global'.
3. IAM users sign-in link, you can 'Customize' and use an alias. 
4. Set-up MFA (Virtual with Google Authenticator App)
5. Create Groups and Users
   	- Have company create an AWS account (root level user, */* permissions).
    - Immediately create IAM group for each department.
    - Create 1 Policy and assign to 1 group, repeat for all.
    - Create new IAM users and assign each to their perspective groups.

## Users
* NOT PASSWORDS -- ACCESS KEY ID and SECRET ACCESS KEYs keep private; allow AWS access via APIs and CLI. Programmatic access.
* Console Password: Used to login to Console.
* Users begin with NO permissions

## Roles
Allow one AWS Service to use another AWS Service. 

## Tips
* Set up MFA on root account.
* Create and customize password rotation policies.

------------------------------------------------------------------------------------------

## Create Billing Alarm
1. Login to AWS Console.
2. CloudWatch service, the Billing Alarm create an SNS Topic (way of emailing you when goes oer a threshold).
#Procedure for AWS IAM 

## Overview
1. Access AWS through AWS Console in browser, AWS SDK, or AWS CLI.
2. Navigate to IAM service and notice the 'region' is 'global'.
3. IAM users sign-in link, you can 'Customize' and use an alias. 
4. Set-up MFA (Virtual with Google Authenticator App)
5. Create Groups and Users
   	- Have company create an AWS account (root level user).
    - Immediately create IAM group for each department.
    - Create 1 Policy and assign to 1 group, repeat for all.
    - Create new IAM users and assign each to their perspective groups.

## Users
* ACCESS KEY and SECRET ACCESS KEY keep private; give access to account.
* Console Password: Used to login to Console.

## Roles
Allow one AWS Service to use another AWS Service. 

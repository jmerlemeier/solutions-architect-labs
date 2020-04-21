#Procedure for AWS IAM 

## Overview
Deploy? Need Servers in Datacenters - took weeks to months.
    The Cloud: provisioning a server in minutes!
It is hitting the AWS APIs 

### New Problem
* Configuring servers
* Managing servers
* Done manually works at small scale, but becomes error-prone at large scale.
  
### Solution
* Automation using custom scripts allows us efficiency and flexibility.
* BUT Custom scripts do not scale
  * Error Prone
  * Difficult to change
  * Not often reusable

### Infastructure as Code !!!
* Basically means you apply dev tools and principles to Infastructure
  * Manage Configurations, Provisioning, Deployments
  * Version Control (git), Testing, CI/CD

### Strengths
1. Cost Reduction
2. Speed
3. Less risk, less chance of human error

### Procedure for Infasructure as Code
1. Template (.yaml or .json)
2. Upload template through Tooling (ex. CloudFormation)
3. CloudFormation handles API calls to the target env
   * Lambda, EC2, S3, Elastic Load Balancing, RDS, VPC
   * also handles changing infastructure 
   * This means I get to worry about the template and not delta changes
   * It manages dependencies
   * Easy Cleanup

### What is AWS CloudFormation??
* free service, but charged for infastructure I provision and maintain
* Manages the lifecycle
  * Create
  * Update
  * Delete

### Provision EC2 Instance 
Type: t2.micro
1. Look at YAML file
```Resources:
  Ec2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-467ca739 # Amazon Linux AMI in N.Virginia
```
1. Go to AWS Console to create stack, CloudFormation
2. Confirm region
3. Click 'create stack'
4. Upload template 
5. Create stack
6. CloudFormation will pass the template and will orchestrate teh EC2 service to provision the t2.micro. Should EC2 instance creation initiated.
7. Go to EC2 service, 'Instances' on L margin - should see instance being provisioned.
8. Once EC2 has confirmed this has started, CloudFormation will get a successful response and the stack will be confirmed as created. 
9. You can see the EC2 Instance Type: t2.micro and the AMI ID is the same as was in the template. 

### UPDATE the stack
1. Lets setup a nametag
2. Create Tags:
```
Resources:
  Ec2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-467ca739 # Amazon Linux AMI in N.Virginia
      Tags:
        - Key: Name
          Value: A simple example
```
3. Updated 

### REMOVE the stack

1. Actions
2. Delete Stack, will see 'DELETE_IN_PROGRESS'
3. Simple. 

-----------------------------------------------------------

### Notes with Stephanie

* Template can be used to create and number of stacks
* it is a constructor function. 
* CloudFormation is a function
* Template has parameters

parameters
resources is the work
!Ref is used to go reference a variable

Template can have outputs. What values do I want to make available in my region. 
Templates are reusable to make multiple stacks.

Example: I make my Networking Space.
1. Here is the VPC ID, ect ect ect 
2. Export contents to be used elsewhere.

CloudFormation is an AWS Service meets language.

### Stacks
* The results of whatever happened in this template. 
* NOT the DS stack
* It knows: Metadata, creation date, name, what template used to create it, parameter values, what resources created by stack, the events that happened while those resources were created, Outputs.

Templates can get long
* Multiple resources: make an instance, make an S3 bucket, make a role.
* DS graph under the hood?

### Vocab
* Template: .yaml or .json text file, blueprint of end state.
* Stacks: CF execites template and creates stack. The stack is a provisione instance of the template.
* Change Set: prior to updating a stack, create change set which allows me to see how changes will impact resources - great for live systems to prevent data loss.

-------------------------------------------------------------------

## Writing Template
* Resources it the only required section.
  * Logial ID for REF inside template
  * Type: 
  * Properties

## EC2
``` 
Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageID: ami-45434534
      InstanceType: t2.micro
```

## S3
```
Resources:
  MyS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: julieBucket
      AccessControl: PublicRead
      WebsiteConfiguration:
        IndexDocument: index.html
```

## Security Group
```
Resources:
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
        - IpProtocol: tcp
        FromPort:'22'
        ToPort: '22'
        Cidrlp:0.0.0.0/0
```

## Intrinsic functions
YAML
`!Join [ delimiter, [ comma-delimited list of values ]]

`!Join[ ":", [a, b, c] ]`

-------------------------------------------------------------------

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
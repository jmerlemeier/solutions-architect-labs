#Procedure for AWS IAM 

## Overview
Deploy? Need Servers in Datacenters - took weeks to months.
    The Cloud: provisioning a server in minutes!

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
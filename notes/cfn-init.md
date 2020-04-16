Resources
- Metadata
    - AWS::CloudFormation::Init:
      - domain-join:
        - files:
          - C:jfjfjfjfjjf
        - download:
          - files:
            - C:\temp\build.zip:
              - source: !Sub https://${S3BucketName}.s3.amazonaws.com/image.jpg


```yaml
Doug's example
#[...]
Resources:
  VirtualMachine: # (could be bananas)
    Type: 'AWS::EC2::Instance'
    Metadata:
      'AWS::CloudFormation::Init':
        config:
          packages:
            yum:
              nginx: []
    Properties:
      #[...] 
      UserData:
        'Fn::Base64': !Sub |
          #!/usr/bin/env bash
          /opt/aws/bin/cfn-init -v --resource VirtualMachine --region ${AWS::Region} --stack ${AWS::StackName}
```

```yaml
Julie's new template
#[...]
Resources:
  VirtualMachine: (could be bananas)
    Type: 'AWS::EC2::Instance'
    Metadata:
      'AWS::CloudFormation::Init':
        config:
          file: #new
    Properties:
      #[...] 
      UserData:
        'Fn::Base64': !Sub |
          #!/usr/bin/env bash
          /opt/aws/bin/cfn-init -v --resource VirtualMachine --region ${AWS::Region} --stack ${AWS::StackName}
```
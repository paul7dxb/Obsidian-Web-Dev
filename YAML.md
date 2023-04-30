- Data-serialization language

# AWS

- Used for infrastructure as code [[19.1 - CloudFormation|AWS CloudFormation]]

# Syntax

```YAML
# Multi line string using "|"
address:
	lines: |
		458 Walkman Rd
		Suite #292

# Arrays / lists using "-"
product:
	- description: basketball
	  quantity: 4
	- description: Shoes
	  quantity: 3

# Reference

```

# Parameters and References

```YAML
# Take in a parameter
Parameters:
  SecurityGroupDescription:
    Description: Security Group Description
    Type: String

# Reference SecurityGroupDescription for EC2 security group
  ServerSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: !Ref SecurityGroupDescription
```

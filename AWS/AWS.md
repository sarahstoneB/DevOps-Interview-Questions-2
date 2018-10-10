# AWS Questions

### General Questions

##### What is an IAM Role?
  An IAM role is an IAM entity that defines a set of permissions for making AWS service requests.
  IAM roles are not associated with a specific user or group. Instead, trusted entities assume roles, such as IAM users, applications, or AWS services such as EC2.

##### What is a NAT Gateway?

A network address translation (NAT) gateway is used to enable instances in a private subnet to connect to the internet or other AWS services, but prevent the internet from initiating a connection with those instances. NAT gateways are created in a public subnet.

##### How do you enable cross account access?
  1. Create an IAM Role in Prod account -> Create role for cross account access -> specify the dev account's ID -> Set permissions for the users
  2. Give users in the Dev account permission to assume the role in the Prod account - > Create a policy and specify the ARN of the prod role

##### What are the differences between security groups in a VPC and network ACLs in a VPC?
  Security groups in a VPC specify which traffic is allowed to or from an Amazon EC2 instance. Network ACLs operate at the subnet level and evaluate traffic entering and exiting a subnet.
  Network ACLs can be used to set both Allow and Deny rules. Network ACLs do not filter traffic between instances in the same subnet.
  In addition, network ACLs perform stateless filtering while security groups perform stateful filtering.

##### Difference between security group and NACL?
 Security Group operates at the instance level and NACL operates at the subnet level
 SG Is stateful - Return traffic is automatically allowed, regardless of any rules and NACL Is stateless - Return traffic must be   explicitly allowed by rules

##### What is VPC peering?
  It is network connection between two VPCs that enables traffic between them.

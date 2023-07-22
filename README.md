# Cloud-BigDataProject

# Introducing the Example Social Research Organization

### Create a new VPC

![VCP](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/118e10c9-7b6f-4d6c-a034-59d8445e3c99)
![VCP2](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/de492b30-b87c-494a-a384-121210c82a2b)

### Create a private subnets

![Subnet](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/477784dc-7bfd-446a-83a1-bef52897ccd4)

### Set up security Group

![SecurityGroup](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/71a10279-b2e4-4bd2-ae4c-6e7aa3cd4987)

### Create database

![CreateDatabase](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/8f703fc3-8b8c-4d55-aae2-89c3a410ef89)
![Database](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/0a007fa6-ba60-4fab-99d4-1718bba4cfe0)

mysql://admin:root1234@database-1.co18woxb7lo7.us-east-1.rds.amazonaws.com:3306/database-1
This is our secure string

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/e1eb7867-f130-4372-9211-b64fcf1d47b9)

### Create EC2

![CreateEC2](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/a5ad7d2a-8995-47fc-92cb-8e499dd717be)

### EC2 security group

![EC2SecurityGroup](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/7b8e5cc6-5dc0-4929-9500-833e2598bee3)

### custom IAM policy

![CreateIAMPolicy](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/f5622ae2-e1f6-4e5a-a7a0-fa953bf1045d)


# QUIZ

There are some images inside **iam quizz** and **network quizz** folder. Your job is to answer the questions by specifying correct answers.
For example if the first option is the correct answer, say **Option 1**

# IAM

## IAM Quizz Part

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/bf14b1d2-b867-4092-9885-f75aca378d30)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/b20b9165-15c4-442f-bc23-96b4034d356e)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/62971dc2-7da0-431d-884e-ee6aee9d6990)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/60417f2c-facf-4fc4-8fcf-fd778ab4b6d7)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/75278597-d2d8-4548-8955-2c9e2445c604)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/75f5fc26-c8e0-491c-ad5c-93c91bfb4bbf)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/89dab3b5-4a39-45d6-bfbc-3ada1f310412)


## Network Quizz Part

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/e4549693-c371-404a-a970-2c239c1c4e11)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/e63005d3-f657-4212-918c-8d64c73297ab)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/768ac34d-fc05-45f2-a9d2-ad3559da4bcb)

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/1dc0ae69-c952-4420-8653-f9658b9277d3)


This part is to make sure you are able to evaluate and apply some policy constraintes.

## Policies evaluation

Please evaluate below IAM policies

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowEC2AndS3",
      "Effect": "Allow",
      "Action": [
        "ec2:RunInstances",
        "ec2:TerminateInstances",
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:ec2:us-east-1:123456789012:instance/*",
        "arn:aws:s3:::example-bucket/*"
      ]
    }
  ]
}
```
This Policy grants permissions that are required to allow EC2 and S3 to do actions according to the courses that are specified. 
Sid: "AllowEC2AndS3": It is a custom identifier.
Effect: "Allow": Specifies that the actions listed are allowed so it basically grants permissions.
Actions: "ec2:RunInstances", "ec2:TerminateInstances", "s3:GetObject", "s3:PutObject": These are the actions that are allowed by the policy. It allows running and terminating EC2 instances, as well as retrieving and uploading objects to an S3 bucket.
Resource: "arn:aws:ec2:us-east-1:123456789012:instance/", "arn:aws:s3:::example-bucket/": Specifies the resources to which the actionswill  apply. The policy allows actions on any EC2 instances in the AWS account located in the region (us-east-1), as well as any objects within the "example-bucket" S3 bucket.



### Question: What actions are allowed for EC2 instances and S3 objects based on this policy? What specific resources are included?

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowVPCAccess",
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeVpcs",
        "ec2:DescribeSubnets",
        "ec2:DescribeSecurityGroups"
      ],
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "aws:RequestedRegion": "us-west-2"
        }
      }
    }
  ]
}
```
Actions allowed for EC2 instances:

ec2:DescribeVpcs: Allows describing VPCs.
ec2:DescribeSubnets: Allows describing subnets.
ec2:DescribeSecurityGroups: Allows describing security groups.
Specific resources included:
"Resource": "*": This policy allows the specified actions (ec2:DescribeVpcs, ec2:DescribeSubnets, and ec2:DescribeSecurityGroups) on any resource within the AWS account. 
### Question: Under what condition does this policy allow access to VPC-related information? Which AWS region is specified?

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowS3ReadWrite",
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::example-bucket",
        "arn:aws:s3:::example-bucket/*"
      ],
      "Condition": {
        "StringLike": {
          "s3:prefix": ["documents/*", "images/*"]
        }
      }
    }
  ]
}
```
Under this policy the access to the VPC-related information is allowed based on the condition "aws:RequestedRegion" which is quite similar to the "us-west-2". This means that the policy only permits VPC-related actions if the API request is made in the designated "us-west-2" AWS region.
Actions allowed for VPC-related information:
ec2:DescribeVpcs: Allows describing VPCs.
ec2:DescribeSubnets: Allows describing subnets.
ec2:DescribeSecurityGroups: Allows describing security groups.
The specified region is "us-west-2". Therefore, this policy will only allow access to VPC-related information when the API request is made in the right "us-west-2" region.

### Question: What actions are allowed on the "example-bucket" and its objects based on this policy? What specific prefixes are specified in the condition?

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowIAMUserCreation",
      "Effect": "Allow",
      "Action": "iam:CreateUser",
      "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
    },
    {
      "Sid": "AllowIAMUserDeletion",
      "Effect": "Allow",
      "Action": "iam:DeleteUser",
      "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
    }
  ]
}
```
Actions allowed for user creation:
iam:CreateUser: Allows creating IAM users.
Actions allowed for user deletion:
iam:DeleteUser: Allows deleting IAM users.
Specific resources:
"Resource": "arn:aws:iam::123456789012:user/${aws:username}": This policy allows the specified actions (iam:CreateUser and iam:DeleteUser) on the IAM user identified by "arn:aws:iam::123456789012:user/${aws:username}". The ${aws:username} serves as a proxy that will be replaced with the actual username of the user making the API request.
This policy allows the creation and deletion of IAM users. The allowed actions are limited to user management within the specified AWS account (123456789012), with the specific IAM user being determined by the requesting user's username.

### Question: What actions are allowed for IAM users based on this policy? How are the resource ARNs constructed?

```json
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": ["iam:Get*", "iam:List*"],
    "Resource": "*"
  }
}
```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": ["iam:Get*", "iam:List*"],
    "Resource": "*"
  }
}
Actions allowed for IAM users:
iam:Get*: Allows IAM users to perform any Get action in IAM, such as iam:GetUser, iam:GetGroup, etc. This action is used to get information about IAM entities and resources.
iam:List*: Allows IAM users to perform any List action in IAM, such as iam:ListUsers, iam:ListGroups, etc. This action is used to list information about IAM entities and resources.
Resource:
"Resource": "*": This policy allows the specified actions (iam:Get* and iam:List*) on any resource that is located in the AWS account. 
In summary, the policy grants IAM users the ability to retrieve and list information about IAM entities and resources within the AWS account. 


### Questions:

- Which AWS service does this policy grant you access to?
- Does it allow you to create an IAM user, group, policy, or role?
- Go to https://docs.aws.amazon.com/IAM/latest/UserGuide/ and in the left navigation expand Reference > Policy Reference > Actions, Resources, and Condition Keys. Choose Identity And Access Management. Scroll to the Actions Defined by Identity And Access Management list.Name at least three specific actions that the **iam:Get\*** action allows.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Condition": {
        "StringEquals": {
          "ec2:InstanceType": ["t2.micro", "t2.small"]
        }
      },
      "Resource": "arn:aws:ec2:*:*:instance/*",
      "Action": ["ec2:RunInstances", "ec2:StartInstances"],
      "Effect": "Deny"
    }
  ]
}
```
The provided IAM policy grants access to the AWS service Identity and Access Management (IAM).
This policy denies the ability to create EC2 instances with specific instance types (t2.micro and t2.small) and start existing instances.
Specific actions allowed by iam:Get* in IAM are:
iam:GetUser: Allows getting information about a specific IAM user.
iam:GetGroup: Allows getting information about a specific IAM group.
iam:GetRole: Allows getting information about a specific IAM role.
These actions are part of the iam:Get* pattern, which allows IAM users to retrieve information about IAM entities and resources.


### Questions:

- What actions does the policy allow?
- Say that the policy included an additional statement object, like this **example:**

```json
{
  "Effect": "Allow",
  "Action": "ec2:*"
}
```

- How would the policy restrict the access granted to you by this additional statement?
- If the policy included both the statement on the left and the statement in question 2, could you terminate an m3.xlarge instance that existed in the account?

The provided IAM policy allows the ec2:* action. This action allows unrestricted access to all EC2 API operations. Therefore, with the additional statement:
The policy grants full permissions for all EC2 actions.
The policy with both statements would grant full EC2 access but explicitly deny (question 2 : ec2:RunInstances and ec2:StartInstances) specific instance types from running or starting instances. In this case we would not be able to terminate an m3.xlarge instance if it gets into the restricted instance types that are defined in the policy.


# Big Data - Data Visualization With AWS QuickSight

### Sum of Cost by category and Admit Date
We add filter in order to have an analyse between 2017 and 2018. We also remove unnecessary category

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/935c20cc-8c80-41da-be1c-939e75172ab5)

### Sum of Revenue/Profit by Admit Date
The graph is focused on the anomalie at déc. 3, 2018 12:00am

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/163d0028-45ef-4640-b97c-d7c357fcd835)

We compare the difference of revenue and profit between 2018 and 2017. There is a positive revenue and a negative profit, we can deduce than 2018 charges and outcome is much highger than 2017 

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/d30b76c7-794d-410c-8a62-316101019023)
![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/2619411b-a160-4bde-bd25-5ed0152086dd)

### Sum of Profit by Hospital
This graph show which hospital have more profit. It allows us to know that it is necessary to create a better balance between hospital in order to split the profit.

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/e65ece09-a2a6-418b-b936-e7325eae94ef)

### Sum of Discount ans Sum of Profit by Category and Admit Date

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/0493b890-ca5d-4e34-b605-bc029c10c368)

### Suggest Analyse

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/6b2225d4-cf72-4d25-8121-09a7c388b596)

### Final Result

![image](https://github.com/Senhua-Liu/Cloud-BigDataProject/assets/73168837/c31041a2-2218-40e9-9d23-8d835d8ed88f)





# ch4
---
## IAM: Users & Groups
- IAM: Identity & Access Management, Global service
- Root account created by default, should not be used or shared
- Users are people within your organization, and can be grouped
- Groups only contain users, not other groups
- Users don't have to belong to a group, and users can belong to multiple groups

## IAM: Permissions
- Users or Groups can be assigned JSON documents called policies
- These policies define the permissions of the users
- In AWS you apply the **least privilege principle**: don't give more permissions than a user needs

## AWS Sign-in Alias
- By default, you have to login using your root account's email address
- You can customize the AWS sign-in url to have your company's name so it's easier to remember and you don't remember account ID

## IAM Policies inheritance
- Users inherit the permissions of the group they belong to

## IAM Policies Structure
```
{
    "Version": "2012-10-17",
    "Id": "S3-Account-Permissions",
    "Statement": [
        {
            "Sid": "S3-Permissions",
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::*"
            ]
        }
    ]
}
```
- Version: policy language version
- Id: an identifier for the policy (Optional)
- Statement: one or more individual statements
  - Sid: an identifier for the statement (Optional)
  - Effect: whether the statement allows or denies access
  - Principal: account/user/role to which this policy applied to
  - Action: list of actions this policy allows or denies
  - Resource: list of resources to which the actions applied to

## IAM - Password Policy
- Strong passwords = higher security for your account
- In AWS, you can setup a password policy:
  - Set a minimum password length
  - Require specific character types
  - Allow all IAM users to change their own passwords
  - Require users to change their password after some time(pw expiration)
  - Prevent password re-use

- Multi Factor Authentication - MFA
    - Users have access to your account password and a unique code from a device that rotates codes every 30 seconds
    - MFA adds a second layer of protection to your account

- MFA devices options in AWS
  - Virtual MFA device: Google Authenticator, Authy
  - Universal 2nd Factor(U2F) Security Key: YubiKey

## IAM Roles for Services
- Some AWS services will need to perform actions on your behalf
- To do so, we will assign permissions to AWS services with IAM Roles
- Common roles:
  - EC2 Instance Roles
  - Lambda Function Roles
  - Roles for CloudFormation
  - Roles for CodeBuild
  - Roles for CodePipeline
  - etc.

## IAM Security Tools
- IAM Credentials Report:(account-level)
  - report that lists all your account's users and the status of their various credentials
- IAM Access Advisor:(user-level)
  - shows the service permissions granted to a user and when those services were last accessed

## IAM Best Practices
- Don't use the root account except for AWS account setup
- One physical user = one AWS user
- Assign users to groups and assign permissions to groups
- Create a strong password policy
- Use and enforce the use of Multi Factor Authentication(MFA)
- Create and use Roles for giving permissions to AWS services
- Use Access Levels for granting permissions to users (CLI, SDK, AWS Management Console)
- Audit permissions of your account with the IAM Credentials Report and Access Advisor
- **Never share IAM users & Access Keys**
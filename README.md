# Ansible-vault-secret-manage-using-AWS-secret-manager

In this article am securing ansible vault encrypt key using AWS secret manager service. Normal we need to remeber the vault encrypt password or we should save it somewhere in server or your local system, and there is no privacy or security to that key, so we save the key in AWS secret manager.

# Prerequisites

- AWS Management Console access
- An instance with installed ansible

# Encrypt ansible yml file

Here I'm going to encrypt variable file on my ansible project

```bash
ansible-vault encrypt variable.yml
```

Then when I'm trying to run the main yml file will get an error like this,


# Create IAM role

Craete IAM role with secret manager read and write policy added in AWS IAM service. Once this role is created, attach it to manager EC2 instance. You can either use custom code for policy or existing policy. You can use this offical documention for [IAM role](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html)

**To create an IAM role using the IAM console**

  1. Open the IAM console at https://console.aws.amazon.com/iam/.
  2. In the navigation panel, choose Roles, Create role.
  3. On the Select role type page, choose EC2 and the EC2 use case. Choose Next: Permissions.
  4. On the Attach permissions policy page, select an AWS managed policy that grants your instances access to the resources that they need.
  5. On the Review page, enter a name for the role and choose Create role.

**To attach an IAM role to an instance**

   1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.
   2. In the navigation pane, choose Instances.
   3. Select the instance, choose Actions, Security, Modify IAM role.
   4. Select the IAM role to attach to your instance, and choose Save.

#  Create secret in secret manager

You can use the AWS console to create the secret details.

**To create a secret**

   1. Open the Secrets Manager console at https://console.aws.amazon.com/secretsmanager/.
   2. Under Secrets, choose Store a new secret.
   3. On the Store a new secret page, do the following:
      a. For Secret type, choose Other type of secret.
      b. For Key/value pairs, in the first field, enter Password. In the second field, enter a password. This will be encrypted when you save the secret.
      c. For Encryption key, keep DefaultEncryptionKey to use the AWS managed key for Secrets Manager. There is no cost for using this key.
      d. Choose Next.
   4. On the Secret name and description page, for Secret name, enter TutorialSecret, and then at the bottom of the page, choose Next.
   5. On the Secret rotation page, keep Disable automatic rotation, and then at the bottom of the page, choose Next.
   6. On the Review page, review the secret details, and then choose Store.

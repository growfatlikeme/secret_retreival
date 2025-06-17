# Retreiving secret from AWS secret manager

## What is needed to authorize your EC2 to retrieve secrets from the AWS Secret Manager?

IAM Role for ec2 to assume, with the policy permitting 2 action "secretsmanager:GetSecretValue" and "secretsmanager:ListSecrets" (optional or remove if not required) to the specific secret ARN.

## Derive the IAM policy (i.e. JSON) using the secret name prod/cart-service/credentials as example

---

arn:aws:secretsmanager:[region]:[account-id]:secret:[secret-name]-[random-suffix]

---

Sample ARN: arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials-\*

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["secretsmanager:GetSecretValue"],
      "Resource": "arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials-*"
    },
    {
      "Effect": "Allow",
      "Action": ["secretsmanager:ListSecrets"],
      "Resource": "*"
    }
  ]
}
```

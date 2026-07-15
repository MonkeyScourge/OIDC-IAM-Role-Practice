# OIDC IAM Role Assumption Demo

Federating Github Actions to assume AWS IAM role via OIDC

## Purpose
This repo demonstrates OIDC authentication granting access to AWS Cloud permissions to GitHub Actions without hard coded secrets. This serves as learning excersize and a practical reference for identity federation

## Why worth learning?
Eliminates static credentials, reducing breach risk. Widely adopted in CI/CD and cloud native security

## Worth Testing?
Misconfigured trust policies or audience claims enable can privelege escalation. Testing makes sure that security boundary is working


## Trust Policy
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Federated": "arn:aws:iam::xxxxxxxxxxxx:oidc-provider/token.actions.githubusercontent.com"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
                "StringEquals": {
                    "token.actions.githubusercontent.com:aud": "sts.amazonaws.com"
                },
                "StringLike": {
                    "token.actions.githubusercontent.com:sub": [
                        "repo:MonkeyScourge/OIDC-IAM-Role-Practice:*",
                        "repo:MonkeyScourge/OIDC-IAM-Role-Practice:*"
                    ]
                }
            }
        }
    ]
}
```


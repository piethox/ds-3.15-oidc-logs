# Module 3.15 Application Logging with Cloudwatch
David Module 3.15 Assignment with OIDC and Cloudwatch Logs on serverless express framework

## What are being used ?
- node.js express
- dependencies : express, jest and serverless
- OpenID Connect for AWS IAM deployment
- Github actions CI/CD pipeline

## Steps
- Create new IAM Identity Provider with token.actions.githubusercontent.com
- Create IAM role on AWS console with proper permission to run the service involved
- Create github workflow

## Reference
For OIDC Setup :

- https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services

- https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/



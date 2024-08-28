# org-formation-cli x GitHub Actions 

## 0. Prerequisites
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [org-formation-cli](https://github.com/org-formation/org-formation-cli)

## 1. Create an OIDC provider for GitHub
```
aws iam create-open-id-connect-provider ‐‐url "https://token.actions.githubusercontent.com" ‐‐client-id-list 'sts.amazonaws.com'
```

## 2. Create IAM role 
Check out the [trust policy for the role](trustPolicyGithubOIDC.json) and use the following command to create the role: 
```
aws iam create-role --role-name github-actions-role --assume-role-policy-document <./path/to/trustPolicyGitHubOIDC.json>
```

### 2.1 Assign minimum level of permissions to IAM role
You can follow [Issue 120](https://github.com/org-formation/org-formation-cli/issues/120#issuecomment-751415550) from the original org-formation-cli [repo](https://github.com/org-formation/org-formation-cli) to setup a set of minimum required permissions. 

## 3. Create GitHub Actions workflow
You can find everything you need in the file [ghas-workflow.yml](ghas-workflow.yml), you will just need to edit it with your information and copy it into ```.github/workflows/```.

## 4. Trigger the workflow
Edit your ```organization.yml``` and then just commit and push your changes. You can check out my [organization.yml](organization.yml), it has 3 Organizational Units (Prod, Test and Dev) and three accounts associated to them. You can also generate a default template using ```org-formation init --region <REGION>``` and personalize it. 


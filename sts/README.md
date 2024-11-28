## sts in the console
1. Created a role *s3AssumeRole*
2. Assign AssumeRole permission for s3 buckets to *s3AssumeRole*
3. Create a user *machine_user*
4. Assign machin_user to role

## sts in cloud formation
**create the stack**
aws cloudformation deploy --template-file template.yaml --stack-name sts-stack --capabilities CAPABILITY_NAMED_IAM --no-execute-changeset

**generate credentials for sts-machine-user**
aws iam create-access-key --user-name sts-machine-user


**set up a profile for sts-machine-user**
aws configure --profile sts-machine-user

**sts-machine-user assume sts-role**
aws sts assume-role --role-arn arn:aws:iam::${account_id}:role/sts-role --role-session-name sts-session --profile sts-machine-user

**confirm assume role**
aws sts get-caller-identity --profile assumeRole

**list s3 buckets using assumeRole profile**
aws s3 ls --profile assumeRole

**clean up**
aws cloudformation delete-stack --stack-name sts-stack





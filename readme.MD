# pod should access aws secret manager
for 18-sa.yaml

search in google as eks ingress controller--> click on github.io--> Deployment--> Installation Guide

REGION_CODE=us-east-1
CLUSTER_NAME=expense
ACC_ID=695862934667(aws account id)

### Permissions

* OIDC provider
It is authentication service to connect the aws and expense cluster(kubernates)

```
eksctl utils associate-iam-oidc-provider \
    --region  us-east-1 \
    --cluster expense \
    --approve
```

2. create policy
3. we need to map sa with IAM policy

```
eksctl create iamserviceaccount \
--cluster=expense \
--namespace=expense \
--name=expense-mysql-secret \
--attach-policy-arn=arn:aws:iam::695862934667:policy/ExpenseMySQLSecretRead \ 
--override-existing-serviceaccounts \
--region us-east-1 \
--approve
```

#--attach-policy-arn=It is the arn of ExpenseMySQLSecretRead policy
eks create service account and attach the IAM role with policy ExpenseMySQLSecretRead.
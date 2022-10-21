**Based on Reference Architecture from = https://www.eksworkshop.com/intermediate/220\_codepipeline/**

**Videos to Follow-Along/Walk-Through Demo:**

We will push code to CodeCommit and CodePipeline will trigger a CodeBuild job to create a container to deploy the yaml file changes to EKS.

\1. Architecture Overview:

This picture is now out-of-date but VERY close.  There is no longer a Lambda function to trigger the deployment, as CodeCommit triggers CodeBuild and CodeBuild will deploy to Kubernetes (EKS).

\2. Steps to Create the CICD Workflow:

1. Create IAM Roles and patch configmap to allow new Pipeline/CodeBuild role to be able to apply changes to EKS.
1. Create an AWS CodeCommit Repo for your app deployment/service
1. Deploy CloudFormation stack to provision Developer Tools resources
1. Optional - Configure dual push to github.domain.com (optional) and AWS CodeCommit
1. Clone sample app files
1. Validate first/initial push to origin master
1. Change your sample code and push again to validate changes to deployment

\3. Create IAM Roles and patch configmap to allow new Pipeline/CodeBuild role to be able to apply changes to EKS.

This can be done via the AWS CLI.  The script to deploy EKS Add-ons performs the following steps.  

*echo "CICD with AWS Developer Tools lab set-up"*

*cd /home/ubuntu*

export ACCOUNT\_ID=$(aws sts get-caller-identity --output text --query Account)

export AWS\_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')

*TRUST="{ \"Version\": \"2012-10-17\", \"Statement\": [ { \"Effect\": \"Allow\", \"Principal\": { \"AWS\": \"arn:aws:iam::${ACCOUNT\_ID}:root\" }, \"Action\": \"sts:AssumeRole\" } ] }"*

*echo '{ "Version": "2012-10-17", "Statement": [ { "Effect": "Allow", "Action": "eks:Describe\*", "Resource": "\*" } ] }' > /tmp/iam-eks-cicd-role-policy*

*aws iam create-role --role-name EKSCodeBuildKubectlRole --assume-role-policy-document "$TRUST" --output text --query 'Role.Arn'*

*aws iam put-role-policy --role-name EKSCodeBuildKubectlRole --policy-name eks-describe --policy-document file:///tmp/iam-eks-cicd-role-policy*

*aws iam get-role --role-name EKSCodeBuildKubectlRole --output text --query 'Role.Arn'*

Copy the above Role ARN to a text editor.

**kubectl edit configmap -n kube-system aws-auth**

Add the following under the maproles section with the Role ARN you copied. Note: this is using system:master for cluster admin RBAC permissions on EKS.

\- rolearn: arn:aws:iam::ACCOUNT\_ID:role/*EKSCodeBuildKubectlRole*
`  `username: build
`  `groups:
`  `- system:masters

\--

**Note: This EKSCodeBuildKubectlRole does not need to be in the cluster-admin RBAC role with system:master privileges.  This can be changed to be for a specific namespace with less permissions.  See AuthN and AuthZ - Integrating LDAP/AD Users to Kubernetes RBAC**

\4. Create an AWS CodeCommit Repo for your app deployment/service

Go to AWS CodeCommit and click Create Repository.  Name it and describe it.

export AWS Keys from go/awsroles

Install git remote codecommit utility

1. https://github.com/aws/git-remote-codecommit
   1. sudo pip install git-remote-codecommit

From a directory on your EKS-Admin EC2 instance with AWS Keys exported.  *git clone HTTPS URL*

*git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true*

\5. Deploy CloudFormation stack to provision Developer Tools resources

Use the following CloudFormation yaml template to deploy your AWS Developer Tools Services (CodePipeline, CodeBuild, Lambda, etc.)

**NOTE: this is using a private VPC, subnet IDs, and a Security Group ID properties that are hard-coded in the CodeBuild resource.  This can be changed to parameters in the template.  Use the same Security Group as your Nodes/Workers in the EKS Cluster.**

**NOTE: the S3 bucket name may be taken already.  Remember S3 is a global namespaces so another account may own it.**

**Also, make sure you use the same CodeCommit repo name you created in the previous step as a parameter input CodeCommitSourceRepo**


\6. (Optional) Configure dual push to github.domain.com and AWS CodeCommit

See instructions on this page:

Git repositories dual push

\7. Clone sample app files

Clone this repo:

https://github.com/rnzsgh/eks-workshop-sample-api-service-go

vi the hello-k8s.yml deployment file to have the Load Balancer be an internal load balancer via an annotation.

annotations:
`  `service.beta.kubernetes.io/aws-load-balancer-internal: "true"
`  `service.beta.kubernetes.io/aws-load-balancer-type: "nlb"

Also, edit source inbound rules for the Security Group by adding ranges under the spec.

loadBalancerSourceRanges:
\- "10.0.0.0/8"

\8. Validate first/initial push to origin master

Install git remote codecommit utility, reference = https://github.com/aws/git-remote-codecommit

**sudo pip install git-remote-codecommit**

Set URL Push Origin to be CodeCommit Repo you created:

**git remote set-url --add --push origin** https://git-codecommit.us-west-2.amazonaws.com/v1/repos/eks-cicd-demo

validate with "git remote -v"

Now push your files to origin master to trigger a CodePipeline build.

git add .

git commit -m "updated service to be internal NLB"

git push -u origin master

Now check CodePipeline to ensure the Source CodeCommit updated and the Build succeeded.

Go to EC2 Load Balancers and find your newly created NLB and grab the DNS record and paste it into a browser to view the web page example saying "Hello World"

\9. Change your sample code and push again to validate changes to deployment

vi the main.go sample app file.  Change the "Hello World" text to read something else and save the file.

git add .

git commit -m "changed message on app"

git push -u origin master

Check that CodePipeline picked up the change in CodeCommit repo and is pushing a new build.

Validate the URL link from NLB DNS name to view the new message once the build completes.


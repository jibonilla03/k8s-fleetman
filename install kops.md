# Install KOps
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops

# Create KOps Group and attach permissions
aws iam create-group --group-name kops

aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonEC2FullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonRoute53FullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/IAMFullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonVPCFullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonSQSFullAccess --group-name kops
aws iam attach-group-policy --policy-arn arn:aws:iam::aws:policy/AmazonEventBridgeFullAccess --group-name kops

# Create KOps user and get login credentials
aws iam create-user --user-name kops

aws iam add-user-to-group --user-name kops --group-name kops

aws iam create-access-key --user-name kops

aws configure --profile kops-cloud-guru-user

export AWS_PROFILE=kops-cloud-guru-user

aws configure list

aws iam list-users

# Create S3 bucket for persistent storage
aws s3api create-bucket \
    --bucket kops-jbonilla-com-state-store \
    --region us-east-1

aws s3api create-bucket \
    --bucket kops-jbonilla-com-oidc-store \
    --region us-east-1 \
    --acl public-read

aws s3api put-bucket-versioning --bucket kops-jbonilla-com-state-store  --versioning-configuration Status=Enabled

aws s3api put-bucket-encryption --bucket kops-jbonilla-com-state-store --server-side-encryption-configuration '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"AES256"}}]}'

# Creating KOps Cluster

export NAME=fleetman.k8s.local
export KOPS_STATE_STORE=s3://kops-jbonilla-com-state-store

aws ec2 describe-availability-zones --region us-east-1

kops create cluster \
    --name=${NAME} \
    --cloud=aws \
    --zones=us-east-1a,us-east-1b,us-east-1c \
    --discovery-store=s3://kops-jbonilla-com-oidc-store/${NAME}/discovery

kops update cluster --name fleetman.k8s.local --yes --admin

# Provision an EKS Cluster

These scripts will provision the following

1. Required VPC and subnets
1. Required security groups
1. EKS cluster + 3 worker nodes in a ASG worker group (Public endpoints)
1. Install nginx-ingress controller with helm
1. Private RDS

## Pre-requisites

After installing the AWS CLI. Configure it to use your credentials.

```shell
$ aws configure
AWS Access Key ID [None]: <YOUR_AWS_ACCESS_KEY_ID>
AWS Secret Access Key [None]: <YOUR_AWS_SECRET_ACCESS_KEY>
Default region name [None]: <YOUR_AWS_REGION>
Default output format [None]: json
```

This enables Terraform access to the configuration file and performs operations on your behalf with these security credentials.

Create a local `terraform.tfvars` file with the following line to set the RDS `admin` user password

```shell
rds_admin_password = "SECURE ADMIN USERPASSWORD"
```

## Terraform Steps

After you've done this, initalize your Terraform workspace, which will download 
the provider and initialize it with the values provided in the `terraform.tfvars` file.

```shell
$ terraform init
```

Then, provision your EKS cluster by running `terraform apply`. This will 
take approximately 10 minutes.

```shell
$ terraform apply
```

## Configure kubectl

```shell
$ aws eks --region ap-southeast-1 update-kubeconfig --name <cluster name>
$ kubectl get nodes
$ helm ls
```

## Things to add

1. Cluster autoscaling
1. Route53 management
1. Private API access
1. Cloudfront
1. RDS read replicas
1. Add more worker group for different instance types or managed groups
1. TLS cert management
1. Bastion host
1. Monitoring and Alerting

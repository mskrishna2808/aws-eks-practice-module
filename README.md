# aws-eks-practice-module

## AWS EKS Cluster Creation

To create an AWS EKS cluster for practice purpose, please use below module

```hcl
module "aws_eks" {
    source = "git::https://github.com/mskrishna2808/aws-eks-practice-module.git?ref=1.0.0"

    eks_cluster_name = "eks_cluster"
    node_group_name  = "eks_cluster_node_group"
    instance_types   = ["t2.micro"]
    ami_type         = "AL2_x86_64"

    cidr_block                = "10.50.0.0/16"
    vpc_name                  = "eks_cluster_vpc"
    availability_zone         = ["us-east-1a", "us-east-1b", "us-east-1c"]
    public_subnet_cidr_blocks = ["10.50.0.0/17", "10.50.128.0/17"]
    public_subnet_name        = "eks_cluster_subnets"

    ec2_instance_name   = "eks_login_instance"
    ami_id              = "ami-09d3b3274b6c5d4aa"
    instance_type       = "t2.micro"
    key_pair_name       = "lab_keypair"

}
```

To see the outputs of ec2 instance follow the below instructions.
1. Create a file called outputs.tf
2. Copy the below content into outputs.tf

```hcl
output "instance_dns_name" {
  value = module.aws_eks.ec2_instance_dns
}

output "instance_ip" {
  value = module.aws_eks.ec2_instance_ip
}

output "endpoint" {
  value = module.aws_eks.endpoint
}

output "kubeconfig-certificate-authority-data" {
  value = module.aws_eks.kubeconfig-certificate-authority-data
}
```
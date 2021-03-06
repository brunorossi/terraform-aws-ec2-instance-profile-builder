# ec2-instance-profile-builder
ec2-instance-profile helps create an instance profile with or without a custom policy(ies). It can add cloudwatch agent rights to IAM as well as ssm, and is often used solely to make a default iam instance profile which gives the privileges needed for cloudwatch agent and ssm to work.

### Example Usage:
Create a default role with permissions for ssm and cloudwatch agent:
```
module "ec2_default_instance_profile" {
  source  = "StratusGrid/ec2-instance-profile-builder/aws"
  version = "2.0.0"
  # source                = "github.com/StratusGrid/terraform-aws-ec2-instance-profile-builder"
  
  instance_profile_name = "${var.name_prefix}-default-ec2-instance-profile${local.full_suffix}"
  input_tags            = merge(local.common_tags, {})
}
```

Create a role with custom permissions in addition to ssm and cloudwatch agent permissions:
```
module "ec2_default_instance_profile" {
  source  = "StratusGrid/ec2-instance-profile-builder/aws"
  version = "2.0.0"
  # source                = "github.com/StratusGrid/terraform-aws-ec2-instance-profile-builder"
  
  instance_profile_name = "${var.name_prefix}-default-ec2-instance-profile${local.full_suffix}"
  custom_policy_jsons    = ["${data.aws_iam_policy_document.my_custom_instance_policy.json}"]
  input_tags            = merge(local.common_tags, {})
}
```
  

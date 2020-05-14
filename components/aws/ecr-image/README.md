
# AWS ECR-Image

`/components/aws/ecr-image`

## Overview


ECR (Elastic Compute Repository) is the private-hosted AWS equivalent of DockerHub.
ECR allows you to securely publish docker images which should not be accessible to external users.

Known Issue (TODO): ECR push requires that CLI credentials at runtime (terraform apply) match with the
project's AWS credentails, as specified in .screts/aws-credentials.

This _might_ help:

```bash
cd dataops-infra
SET AWS_SHARED_CREDENTIALS_FILE=($pwd)/.secrets/aws-credentials
SET AWS_PROFILE=default
cd infra
terraform apply
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:-----:|
| environment | Standard `environment` module input. | <pre>object({<br>    vpc_id          = string<br>    aws_region      = string<br>    public_subnets  = list(string)<br>    private_subnets = list(string)<br>  })</pre> | n/a | yes |
| is\_disabled | Switch for disabling ECR image and push. | `bool` | n/a | yes |
| name\_prefix | Standard `name_prefix` module input. | `string` | n/a | yes |
| repository\_name | Name of Docker repository. | `string` | n/a | yes |
| resource\_tags | Standard `resource_tags` module input. | `map(string)` | n/a | yes |
| source\_image\_path | Path to Docker image source. | `string` | n/a | yes |
| tag | Tag to use for deployed Docker image. | `string` | `"latest"` | no |

## Outputs

| Name | Description |
|------|-------------|
| ecr\_image\_url | The full path to the ECR image, including image name. |
| ecr\_image\_url\_and\_tag | The full path to the ECR image, including image name and tag. |
| ecr\_repo\_arn | The unique ID (ARN) of the ECR repo. |
| ecr\_repo\_root | The path to the ECR repo, excluding image name. |

---------------------

## Source Files

_Source code for this module is available using the links below._

* [main.tf](main.tf)
* [outputs.tf](outputs.tf)
* [variables.tf](variables.tf)

---------------------

_**NOTE:** This documentation was auto-generated using
`terraform-docs` and `s-infra` from `slalom.dataops`.
Please do not attempt to manually update this file._
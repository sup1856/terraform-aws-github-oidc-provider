# Github OIDC Provider

This module setups an AWS OIDC Identity prodiver for Github Actions.  This will allow you to use OIDC Federation to give your
Github Actions access to your AWS account.

Main Doc: https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services

## Filtering on the `sub`
Conditions to validate

Doc: https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect#examples

This controls can help you do things like:
* Only allow a certain branch
* Only allow a certain repo/org

## ARN to use in the Github Actions
This module outputs an `arn` value.  This is the `arn` you should use in the Github Actions.

<!-- BEGIN_TF_DOCS -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_iam_assumable_role_admin"></a> [iam\_assumable\_role\_admin](#module\_iam\_assumable\_role\_admin) | terraform-aws-modules/iam/aws//modules/iam-assumable-role-with-oidc | 3.6.0 |

## Resources

| Name | Type |
|------|------|
| [aws_iam_openid_connect_provider.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_openid_connect_provider) | resource |
| [aws_iam_policy.iam_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_aws_policy_json"></a> [aws\_policy\_json](#input\_aws\_policy\_json) | The AWS policy in a json format | `string` | `"{\n    \"Version\": \"2012-10-17\",\n    \"Statement\": [\n      {\n        \"Effect\": \"Allow\",\n        \"Action\": \"*\",\n        \"Resource\": \"*\"\n      }\n    ]\n}\n"` | no |
| <a name="input_client_id_list"></a> [client\_id\_list](#input\_client\_id\_list) | n/a | `list` | <pre>[<br>  "sts.amazonaws.com"<br>]</pre> | no |
| <a name="input_create_identity_provider"></a> [create\_identity\_provider](#input\_create\_identity\_provider) | This switch allows you to create or not create the identity provider.  Only one can exist.  If you are creating multiple Github OIDC Federations, only one of the instantiations should create this or the Terraform run will fail. | `bool` | `true` | no |
| <a name="input_name"></a> [name](#input\_name) | The name for the various resources | `string` | `"github_oidc"` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Tags | `map(any)` | `{}` | no |
| <a name="input_thumbprint_list"></a> [thumbprint\_list](#input\_thumbprint\_list) | This is the thumbprint returned if you were to create an "identity provider" in AWS and gave it this url: https://token.actions.githubusercontent.com | `list` | <pre>[<br>  "a031c46782e6e6c662c2c87c76da9aa62ccabd8e"<br>]</pre> | no |
| <a name="input_url"></a> [url](#input\_url) | n/a | `string` | `"https://token.actions.githubusercontent.com"` | no |
| <a name="input_validate_conditions"></a> [validate\_conditions](#input\_validate\_conditions) | Conditions to validate | `set(string)` | <pre>[<br>  "repo:octo-org/octo-repo:ref:refs/heads/octo-branch"<br>]</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | n/a |
<!-- END_TF_DOCS -->
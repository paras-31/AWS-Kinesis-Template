# ceq_tf_template_aws_kinesis_sample

Configuration in this directory creates Aws Kinesis data stream

## Usage

To run this example you need to execute:

```bash
# Terraform Plan/Apply Pipeline

This GitHub Actions workflow automates the Terraform plan and apply process for infrastructure provisioning and management in AWS.

## Workflow Overview

This workflow consists of two main jobs:

1. **terraform-plan**: This job checks out the repository, sets up Terraform, initializes Terraform, runs a Terraform plan, converts the plan to JSON format, uploads the JSON plan to artifacts, and runs Infracost for cost estimation.

2. **terraform-apply**: This job is dependent on the `terraform-plan` job. It checks out the repository, configures AWS credentials, sets up Terraform, initializes Terraform, and applies the Terraform changes.

## Environment Variables

- `REGION`: The AWS region where the infrastructure will be provisioned.

## Secrets

- `AWS_WAR_REMIDIATION_SANDBOX_ACCESS_KEY`: Access key for AWS IAM user with permissions to manage infrastructure.
- `AWS_WAR_REMIDIATION_SANDBOX_SECRET_KEY`: Secret key for AWS IAM user.
- `CEQ_GHREPOSVCUSER_PAT_TOKEN`: Personal access token for accessing the repository.
- `API_TOKEN`: API_TOKEN for Trend Vision Micro to estimate potential security issues or configurations.
-  To get an API Token from Trend Vision One, follow these steps:
    Log in to Trend Vision One: Go to the Trend Vision One console and log in with your credentials.
    Navigate to API Management: Once logged in, go to the "Administration" or "Settings" section. Look for "API Management" or a similar option.
    Create a New API Key: In the API Management section, there should be an option to create a new API key. Click on it.
    Configure API Key Settings: You may need to specify details such as the name of the API key, permissions, and scope. Configure these settings according to
    your needs.
    Generate the API Key: After configuring the settings, click on the "Generate" or "Create" button to generate the API key.
    Save the API Key: Once generated, the API key will be displayed. Make sure to copy and save it securely as you may not be able to view it again later

## Usage

1. Fork this repository.
2. Set up the required secrets in your repository settings.
3. Modify the workflow file as needed for your specific infrastructure and requirements.
4. Commit and push your changes to trigger the workflow.
5. Monitor the workflow execution and review the Terraform plan before applying changes.


```

Note that this example may create resources which can cost money. Run `terraform destroy` when you don't need these resources.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

| Name                                                                     | Version |
| ------------------------------------------------------------------------ | ------- |
| <a name="requirement_terraform"></a> [terraform](#requirement_terraform) | >= 1.0  |
| <a name="requirement_aws"></a> [aws](#requirement_aws)                   | >= 4.66 |

## Providers

| Name                                             | Version |
| ------------------------------------------------ | ------- |
| <a name="provider_aws"></a> [aws](#provider_aws) | >= 4.66 |

## Modules

| Name                                                          | Source                                                         | Version |
| ------------------------------------------------------------- | -------------------------------------------------------------- | ------- |
| <a name="AWS KINESIS"></a> [AWS KINESIS](#module_AWS_KINESIS) | https://github.com/cloudeq-EMU-ORG/ceq_tf_template_aws_kinesis | n/a     |

## Resources

| Name                        | Type     |
| --------------------------- | -------- |
| aws_kinesis_stream          | resource |
| aws_kinesis_stream_consumer | resource |

## Inputs

| Variable Name               | Description                                                                                      | Type           | Default                              |
| --------------------------- | ------------------------------------------------------------------------------------------------ | -------------- | ------------------------------------ |
| `shard_count`               | The number of shards that the stream will use                                                    | `number`       | `1`                                  |
| `retention_period`          | Length of time data records are accessible after they are added to the stream (24 - 168 hours)   | `number`       | `24`                                 |
| `shard_level_metrics`       | A list of shard-level CloudWatch metrics which can be enabled for the stream                     | `list(string)` | `["IncomingBytes", "OutgoingBytes"]` |
| `enforce_consumer_deletion` | Indicates whether to deregister all registered consumers so that the stream can be destroyed     | `bool`         | `false`                              |
| `encryption_type`           | The encryption type to use. Acceptable values are `NONE` and `KMS`                               | `string`       | `KMS`                                |
| `kms_key_id`                | The GUID for the customer-managed KMS key to use for encryption                                  | `string`       | `alias/aws/kinesis`                  |
| `stream_mode`               | Specifies the capacity mode of the stream (`PROVISIONED` or `ON_DEMAND`). Ignored if `ON_DEMAND` | `string`       | `null`                               |
| `consumer_count`            | Number of consumers to register with Kinesis stream                                              | `number`       | `0`                                  |
| `enabled`                   | Whether the Kinesis stream is enabled                                                            | `bool`         | `true`                               |
| `name`                      | The name of the Kinesis stream                                                                   | `string`       |                                      |
| `tags`                      | A mapping of tags to assign to the Kinesis stream                                                | `map(any)`     |                                      |

## Outputs

| Name                                                                  | Description                                       |
| --------------------------------------------------------------------- | ------------------------------------------------- |
| <a name="output_name"></a> [acm_name](#output_names)                  | Name of the Kinesis stream.                       |
| <a name="output_shard_count"></a> [shard_count](#output_shard_count)  | Number of shards provisioned.                     |
| <a name="output_stream_arn"></a> [acm_stream_arn](#output_stream_arn) | ARN of the Kinesis stream.                        |
| <a name="output_consumers"></a> [consumers](#output_consumers)        | List of consumers registered with Kinesis stream. |

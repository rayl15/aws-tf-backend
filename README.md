# Terraform AWS Backend Module

This Terraform module provisions an AWS backend setup for managing state and locking in a secure and efficient manner using AWS resources. It includes the creation of an S3 bucket for state storage, DynamoDB table for state locking, KMS key for encryption, and AWS Resource Group for managing and tagging resources.

## Features

- **Secure S3 Bucket for State Storage**: The module provisions an S3 bucket with server-side encryption (via AWS KMS) and versioning for storing Terraform state files securely.
- **DynamoDB Table for State Locking**: Prevents simultaneous state changes by enabling state locking using a DynamoDB table.
- **Random Namespace Generation**: Ensures the uniqueness of resource names by appending a random 24-character string to the namespace.
- **AWS Resource Group**: Groups and manages AWS resources using AWS Resource Groups, allowing better tracking through tagging.

## Architecture Overview

This module sets up the following AWS resources:
- **AWS S3 Bucket**: For storing Terraform state files with KMS encryption and versioning enabled.
- **AWS DynamoDB Table**: Used for Terraform state locking to ensure no concurrent operations modify the state file.
- **AWS KMS Key**: Encrypts the S3 bucket's content to enhance security.
- **AWS Resource Group**: A group to organize and tag resources for easy management.
  
## Usage

### Example

```
hcl
module "aws_backend" {
  source              = "path_to_this_module"
  namespace           = "my-app"
  force_destroy_state = true
}
```


### Inputs

| Name                  | Type     | Description                                         | Default |
|-----------------------|----------|-----------------------------------------------------|---------|
| `namespace`           | `string` | A base namespace for naming and tagging resources.  | n/a     |
| `force_destroy_state`  | `bool`   | Whether to forcefully delete the S3 bucket on destroy. | `false` |

### Outputs

| Name              | Description                                   |
|-------------------|-----------------------------------------------|
| `s3_bucket_id`    | The ID of the created S3 bucket.              |
| `dynamodb_table`  | The name of the created DynamoDB table.       |
| `kms_key_arn`     | The ARN of the KMS key for encryption.        |
| `resource_group`  | The name of the AWS Resource Group created.   |


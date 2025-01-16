# Unused IAM Policies Plugin

## Overview

The Unused IAM Policies Plugin identifies IAM policies with zero attachments, helping to optimize IAM policy management by identifying policies that can be deleted or reviewed.

### Commands to install the plugin
to install the plugin use the following command
```bash
uv add opsbox-iam-checks
```
to install the plugin as part of the AWS bundle use the following command
```bash
uv add "opsbox[aws]"
```
## Key Features

- **AWS IAM Integration**: Fetches and processes data from AWS IAM.
- **Optimization Recommendations**: Identifies unused IAM policies to optimize policy management.
- **Detailed Analysis**: Provides detailed information on IAM policies with zero attachments.

## Configuration Parameters

### AWS Configuration

- **aws_access_key_id**: AWS access key ID.
- **aws_secret_access_key**: AWS secret access key.
- **aws_region**: AWS region.

## Example Configuration

```yaml
aws_access_key_id: your_access_key_id
aws_secret_access_key: your_secret_access_key
aws_region: your_aws_region
```

# No Healthy Targets

## Overview

The No Healthy Targets check identifies elbs where all targets are unhealthy. 

## Key Features

- **AWS ELB Integration**: Fetches and processes data from AWS ELB.
- **Inactive Resource Identification**: Identifies load balancers that have no healthy targets.

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
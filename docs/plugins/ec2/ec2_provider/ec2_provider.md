# EC2Provider

### Overview
The EC2Provider plugin collects detailed information about AWS EC2 instances, including their associated volumes and Elastic IP addresses, to facilitate monitoring and management.

### Commands to install the plugin
To install the plugin individually use the following command, simply add the `opsbox-ec2-provider` package to your project.
This can be done through pip or uv.

!!! info

    This plugin is *automatically installed* as part of the Opsbox EC2 check collection, installable with the `opsbox-ec2-checks` package.

### Fields
| Field Name            | Type                | Description                             | Required | Default |
|-----------------------|---------------------|-----------------------------------------|----------|---------|
| aws_access_key_id     | str                 | AWS access key ID                       | Yes      | -       |
| aws_secret_access_key | str                 | AWS secret access key                   | Yes      | -       |
| aws_region            | str \| None         | AWS region                              | No       | None    |
| volume_tags           | str \| None         | Key-value tag pairs for volumes         | No       | None    |
| instance_tags         | str \| None         | Key-value tag pairs for instances       | No       | None    |
| eip_tags              | str \| None         | Key-value tag pairs for Elastic IPs     | No       | None    |

## RDSProvider

### Overview
The RDSProvider plugin collects information about AWS RDS instances to help manage and optimize database performance and cost.

### Commands to install the plugin
To install the plugin individually use the following command, simply add the `opsbox-rds-provider` package to your project.


!!! info

    This plugin is *automatically installed* as part of the Opsbox ELB check collection, installable with the `opsbox-rds-checks` package.


### Fields

| Field                  | Type   | Description                | Required | Default |
|------------------------|--------|----------------------------|----------|---------|
| aws_access_key_id      | string | AWS access key ID          | Yes      | -       |
| aws_secret_access_key  | string | AWS secret access key      | Yes      | -       |
| aws_region             | string | AWS Region                 | No       | None    |


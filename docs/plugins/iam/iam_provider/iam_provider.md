## IAMProvider

### Overview
The IAMProvider plugin collects data related to AWS IAM, including information about users, groups, and roles, to help manage access and permissions effectively.

### Commands to install the plugin
To install the plugin individually use the following command, simply add the `opsbox-iam-provider` package to your project.


!!! info

    This plugin is *automatically installed* as part of the Opsbox ELB check collection, installable with the `opsbox-aws-iam-checks` package.


### Fields

| Field                  | Type   | Description                | Required | Default |
|------------------------|--------|----------------------------|----------|---------|
| aws_access_key_id      | string | AWS access key ID          | Yes      | -       |
| aws_secret_access_key  | string | AWS secret access key      | Yes      | -       |
| aws_region             | string | AWS Region                 | No       | None    |

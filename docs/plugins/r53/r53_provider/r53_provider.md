## Route53Provider

### Overview
The Route53Provider plugin collects data related to AWS Route53, including information about hosted zones, records, and health checks, to help manage DNS and routing effectively.

### Commands to install the plugin
To install the plugin individually use the following command, simply add the `opsbox-r53-provider` package to your project.
This can be done through pip or uv.

!!! info

    This plugin is *automatically installed* as part of the Opsbox Route53 check collection, installable with the `opsbox-r53-checks` package.


### Fields

| Field                  | Type   | Description                | Required | Default |
|------------------------|--------|----------------------------|----------|---------|
| aws_access_key_id      | string | AWS access key ID          | Yes      | -       |
| aws_secret_access_key  | string | AWS secret access key      | Yes      | -       |
| aws_region             | string | AWS Region                 | No       | None    |



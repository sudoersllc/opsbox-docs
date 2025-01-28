## ELBProvider

### Overview
The ELBProvider plugin gathers comprehensive data about AWS Elastic Load Balancers, including Classic, Application, and Network Load Balancers, to optimize performance and identify potential issues.

### Commands to install the plugin
To install the plugin individually use the following command, simply add the `opsbox-elb-provider` package to your project.
This can be done through pip or uv.

!!! info

    This plugin is *automatically installed* as part of the Opsbox ELB check collection, installable with the `opsbox-elb-checks` package.


### Fields

| Field                  | Type   | Description                | Required | Default |
|------------------------|--------|----------------------------|----------|---------|
| aws_access_key_id      | string | AWS access key ID          | Yes      | -       |
| aws_secret_access_key  | string | AWS secret access key      | Yes      | -       |
| aws_region             | string | AWS Region                 | No       | None    |


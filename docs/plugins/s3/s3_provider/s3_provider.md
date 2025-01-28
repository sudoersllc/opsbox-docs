
## S3Provider

### Overview
The S3Provider plugin gathers data related to AWS S3, including information about buckets, objects, and storage classes, to assist in storage management and cost optimization.

### Commands to install the plugin
To install the plugin individually use the following command, simply add the `opsbox-s3-provider` package to your project.


!!! info

    This plugin is *automatically installed* as part of the Opsbox Route53 check collection, installable with the `opsbox-s3-checks` package.


### Fields

| Field                  | Type   | Description                | Required | Default |
|------------------------|--------|----------------------------|----------|---------|
| aws_access_key_id      | string | AWS access key ID          | Yes      | -       |
| aws_secret_access_key  | string | AWS secret access key      | Yes      | -       |
| aws_region             | string | AWS Region                 | No       | None    |

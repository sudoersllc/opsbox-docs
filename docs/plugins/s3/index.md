# Opsbox S3 Check Collection

Opsbox has a collection of rego checks to monitor various aspects of your S3 environment.

| Check Name                        | Description                                                        | Pipeline Name          |
|-----------------------------------|--------------------------------------------------------------------|------------------------|
| Unused Buckets                    | Identifies S3 buckets that have not been accessed or modified for a specified period. | `unused_buckets`       |
| Object Last Modified              | Checks the last modified date of objects in S3 buckets.            | `object_last_modified` |
| Storage Class Usage               | Monitors the usage of different storage classes in S3 buckets.     | `storage_class_usage`  |

!!! note "Installation Collection Package Name"

    `opsbox-s3-checks` is the name of this collection.

    To install any of the S3 checks in this collection, install this collection by adding `opsbox-s3-checks` to your project.

    *These checks rely on the S3 Provider, which is installed as a prerequisite of this package.*
    *More info on the S3 provider can be found [here](./s3_provider/s3_provider.md)*

You can find more details about each check in their respective documentation files.
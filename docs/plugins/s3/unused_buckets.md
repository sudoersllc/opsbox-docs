# Unused Buckets Plugin

## Overview

The Unused Buckets Plugin identifies S3 buckets that have not been accessed or modified for a specified period, helping to optimize storage costs by identifying buckets that can be deleted or archived.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community S3 checks, installable by adding `opsbox-s3-checks` to your project.

## Features

- Fetches and processes data from AWS S3.
- Identifies unused buckets that can be deleted or archived to save costs.

## Configuration Parameters
Besides [provider configuration](./s3_provider/s3_provider.md#fields),


| Parameter                          | Type     | Default Value                          | Description                                                                 |
|------------------------------------|----------|----------------------------------------|-----------------------------------------------------------------------------|
| s3_unused_bucket_date_threshold    | datetime | (datetime.now() - timedelta(days=90))  | How long ago a bucket has to have been last used for it to be considered unused. Default is 90 days. |


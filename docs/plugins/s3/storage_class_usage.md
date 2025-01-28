# Storage Class Usage Plugin

## Overview

The Storage Class Usage Plugin identifies S3 buckets using specific storage classes (e.g., GLACIER, STANDARD), helping to optimize storage costs by recommending appropriate storage classes based on usage patterns.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community S3 checks, installable by adding `opsbox-s3-checks` to your project.

## Features
- Fetches and processes data from AWS S3.
- Identifies buckets that can benefit from different storage classes to save costs.

## Configuration Parameters
Besides [provider configuration](./s3_provider/s3_provider.md#fields),

| Parameter                         | Type     | Default Value                          | Description                                                                 |
|-----------------------------------|----------|----------------------------------------|-----------------------------------------------------------------------------|
| s3_stale_bucket_date_threshold    | datetime | (datetime.now() - timedelta(days=90))  | How long ago a bucket has to have been last used for it to be considered stale. Default is 90 days.               |

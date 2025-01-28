# Object Last Modified Plugin

## Overview

The Object Last Modified Plugin identifies S3 objects that have not been modified for a specified period, helping to optimize storage costs by identifying objects that can be deleted or archived.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community S3 checks, installable by adding `opsbox-s3-checks` to your project.

## Features

- Fetches and processes data from AWS S3.
- Identifies objects that can be deleted or archived to save costs.

## Configuration Parameters
Besides [provider configuration](./s3_provider/s3_provider.md#fields),

| Parameter                        | Type     | Default Value                         | Description                                                                 |
|----------------------------------|----------|---------------------------------------|-----------------------------------------------------------------------------|
| s3_last_modified_date_threshold | datetime | `datetime.now() - timedelta(days=90)` | How long ago an object has to remain unmodified for it to be considered old. Default is 90 days. |
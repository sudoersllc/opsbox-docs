# Old Snapshots Plugin

## Overview

The Old Snapshots Plugin identifies old RDS snapshots that are no longer needed, helping to reduce storage costs by deleting outdated snapshots.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community RDS checks, installable by adding `opsbox-rds-checks` to your project.

## Features

- Fetches and processes data from AWS RDS.
- Identifies old snapshots that can be deleted to save storage costs.

## Configuration Parameters

Besides [provider configuration](./rds_provider/rds_provider.md#fields),

| Parameter                | Type     | Default Value                        | Description                                                                 |
|--------------------------|----------|--------------------------------------|-----------------------------------------------------------------------------|
| `rds_old_date_threshold` | datetime | (datetime.now() - timedelta(days=90)) | How long ago a snapshot was created to be considered old. Default is 90 days. |

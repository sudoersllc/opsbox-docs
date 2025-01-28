# Empty Storage Plugin

## Overview

The Empty Storage Plugin identifies RDS instances with empty storage, helping to optimize storage usage and reduce costs by identifying instances that can be resized or terminated.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community RDS checks, installable by adding `opsbox-rds-checks` to your project.

## Key Features

- Fetches and processes data from AWS RDS.
- Identifies RDS instances with empty storage that can be resized or terminated to save costs.

## Configuration Parameters
Besides [provider configuration](./rds_provider/rds_provider.md#fields),

| Parameter                    | Type   | Default | Description                                                                 |
|------------------------------|--------|---------|-----------------------------------------------------------------------------|
| rds_empty_storage_threshold  | int    | 40      | % of storage utilization under which an RDS instance is flagged as empty. Default = 40. |


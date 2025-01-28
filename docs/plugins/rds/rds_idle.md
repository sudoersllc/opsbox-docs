# RDS Idle Plugin

## Overview

The RDS Idle Plugin identifies idle RDS instances, helping to optimize resource usage and reduce costs by identifying instances that can be stopped or terminated.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community RDS checks, installable by adding `opsbox-rds-checks` to your project.

## Key Features

- Fetches and processes data from AWS RDS.
- Identifies idle RDS instances that can be stopped or terminated to save costs.

## Configuration Parameters

Besides [provider configuration](./rds_provider/rds_provider.md#fields),

| Parameter                  | Type           | Default | Description                                                                 |
|----------------------------|----------------|---------|-----------------------------------------------------------------------------|
| `rds_cpu_idle_threshold`   | Annotated[int] | 5       | % of CPU utilization under which an RDS instance is flagged as idle. Default = 5. |


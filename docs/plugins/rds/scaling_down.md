# Scaling Down RDS Instances

## Overview

Scaling down RDS instances involves reducing the allocated resources (such as CPU, memory, or storage) to better match the current workload. This can help optimize costs and improve resource utilization.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community RDS checks, installable by adding `opsbox-rds-checks` to your project.

## Key Features

- Recommends adjusting the instance size to better fit the workload.
- Reduces costs by allocating fewer resources.

## Configuration Parameters
Besides [provider configuration](./rds_provider/rds_provider.md#fields),

| Parameter                  | Type  | Default | Description                                                                 |
|----------------------------|-------|---------|-----------------------------------------------------------------------------|
| rds_cpu_scaling_threshold  | int   | 20      | % of CPU utilization under which an RDS instance is recommended to scale down. Default = 20. |


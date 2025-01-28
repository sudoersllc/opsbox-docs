
# Low Request Count Load Balancers

## Overview

The Low Request Count Load Balancers check identifies load balancers with low request counts.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community ELB checks, installable by adding `opsbox-elb-checks` to your project.

## Key Features

- Fetches and processes data from AWS ELB.
- Identifies load balancers with low request counts.

## Configuration Parameters
Besides [provider configuration](./elb_provider/elb_provider.md#fields),

| Parameter                  | Type  | Default | Description                                                                 |
|----------------------------|-------|---------|-----------------------------------------------------------------------------|
| elb_low_requests_threshold | int   | 100     | # of requests below which to consider an ELB to have low request counts.    |



# Inactive Load Balancers

## Overview

The Inactive Load Balancers check identifies load balancers that are inactive.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community ELB checks, installable by adding `opsbox-elb-checks` to your project.

## Features

- Fetches and processes data from AWS ELB.
- Identifies load balancers that are inactive.
- Recommends decommissioning inactive load balancers to save costs.

## Configuration Parameters
Besides [provider configuration](./elb_provider/elb_provider.md#fields),

| Parameter                        | Type | Default | Description                                                                 |
|----------------------------------|------|---------|-----------------------------------------------------------------------------|
| elb_inactive_requests_threshold  | int  | 0       | # of requests below which to consider an ELB to be inactive. Default = 0.   |


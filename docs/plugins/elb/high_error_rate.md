# High Error Rate Load Balancers

## Overview

The High Error Rate Load Balancers check identifies load balancers with a high error rate.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community ELB checks, installable by adding `opsbox-elb-checks` to your project.

## Features

- Fetches and processes data from AWS ELB.
- Identifies load balancers with high error rates.

## Configuration Parameters
Besides [provider configuration](./elb_provider/elb_provider.md#fields),

| Parameter                | Type  | Default | Description                                                                 |
|--------------------------|-------|---------|-----------------------------------------------------------------------------|
| elb_error_rate_threshold | int   | 0       | # of errors needed to consider an ELB to have a high error rate.            |
# Idle Instances Plugin

## Overview

The Idle Instances Plugin identifies EC2 instances that are running but have low utilization, helping to reduce costs by stopping or terminating these instances.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community EC2 checks, installable by adding `opsbox-ec2-checks` to your project.

## Features

- Fetches and processes data from AWS EC2.
- Identifies instances that can be stopped or terminated to save costs.
- Provides detailed information on low-utilized EC2 instances.

## Configuration Parameters
Besides [provider configuration](./ec2_provider/ec2_provider.md#fields),

| Parameter | Type | Default Value | Description |
|-----------|------|---------|-------------|
| `ec2_cpu_idle_threshold` | int | 1 | The % threshold for the average CPU utilization of an EC2 instance to be considered idle. Default is 1. |

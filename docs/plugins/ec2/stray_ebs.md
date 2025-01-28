# Stray EBS Volumes Plugin

## Overview

The Stray EBS Volumes Plugin identifies EBS volumes that are not attached to any instances, helping to reduce costs by deleting unused volumes.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community EC2 checks, installable by adding `opsbox-ec2-checks` to your project.

## Features

- Fetches and processes data from AWS EC2.
- Identifies EBS volumes that can be deleted to save costs.

## Configuration Parameters
Besides [provider configuration](./ec2_provider/ec2_provider.md#fields), there are none.

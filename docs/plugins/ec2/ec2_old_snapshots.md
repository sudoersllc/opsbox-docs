# Old EC2 Snapshots Plugin

## Overview

The Old EC2 Snapshots Plugin identifies EC2 snapshots that are older than a specified period, helping to optimize storage costs by identifying snapshots that can be deleted or archived.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community EC2 checks, installable by adding `opsbox-ec2-checks` to your project.

## Features
- Fetches and processes data from AWS EC2.
- Identifies old snapshots that can be deleted or archived to save costs.
- Provides detailed information on old EC2 snapshots.

## Configuration Parameters
Besides [provider configuration](./ec2_provider/ec2_provider.md#fields),

| Parameter                    | Type     | Default Value                          | Description                                                                 |
|------------------------------|----------|----------------------------------------|-----------------------------------------------------------------------------|
| ec2_snapshot_old_threshold   | datetime | `datetime.now() - timedelta(days=90)`  | How long ago a snapshot was created to be considered old. Default is 90 days. |
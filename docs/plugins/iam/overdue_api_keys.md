# Overdue API Keys Plugin

## Overview

The Overdue API Keys Plugin identifies IAM API keys that are overdue, helping to enhance security by ensuring all API keys are rotated regularly.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community IAM checks, installable by adding `opsbox-aws-iam-checks` to your project.

## Features

- Fetches and processes data from AWS IAM.
- Identifies overdue API keys to improve security.

## Configuration Parameters
Besides [provider configuration](./ec2_provider/ec2_provider.md#fields),


| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `iam_overdue_key_date_threshold` | `datetime` | `datetime.now() - timedelta(days=90)` | How long ago a key was last used for it to be considered overdue. Default is 90 days. |

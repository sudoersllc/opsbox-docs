# Unused IAM Policies Plugin

## Overview

The Unused IAM Policies Plugin identifies IAM policies with zero attachments, helping to optimize IAM policy management by identifying policies that can be deleted or reviewed.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community IAM checks, installable by adding `opsbox-aws-iam-checks` to your project.

## Features

- Fetches and processes data from AWS IAM.
- Provides detailed information on IAM policies with zero attachments.

## Configuration Parameters
Besides [provider configuration](./iam_provider/iam_provider.md#fields),

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| iam_unused_attachment_threshold | int | 0 | The number of attachments a policy must have to be considered used. Default is 0. |

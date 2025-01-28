# Unattached EIPs Plugin

## Overview

The Unattached EIPs Plugin identifies Elastic IPs (EIPs) that are not associated with any running instances, helping to reduce costs by releasing unused EIPs.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community EC2 checks, installable by adding `opsbox-ec2-checks` to your project.

## Features

- Fetches and processes data from AWS EC2.
- Identifies EIPs that can be released to save costs.

## Configuration Parameters
Besides [provider configuration](./ec2_provider/ec2_provider.md#fields), there are none.

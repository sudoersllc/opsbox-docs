# Empty Route 53 Hosted Zones Plugin

## Overview

The Empty Route 53 Hosted Zones Plugin identifies Route 53 hosted zones with no DNS records, helping to optimize DNS management by identifying zones that can be deleted or reviewed.

!!! info "Bundled Check"

    This check is bundled alongside the rest of the community Route53 checks, installable by adding `opsbox-r53-checks` to your project.

## Features

- Fetches and processes data from AWS Route 53.
- Provides detailed information on Route 53 hosted zones with no DNS records.

## Configuration Parameters
Besides [provider configuration](./r53_provider/r53_provider.md#fields), there are none.
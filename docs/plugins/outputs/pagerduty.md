# PagerDutyOutput Plugin

## Overview

The PagerDutyOutput Plugin processes and sends results to PagerDuty, allowing for incident creation and management based on the findings.

### Commands to install the plugin
to install the plugin use the following command
```bash
uv add opsbox-pagerduty-output
```

***Description creation requires LLM***

## Key Features

- **PagerDuty Integration**: Sends results to PagerDuty.
- **Customizable Incident Creation**: Allows specifying whether to create a description or an issue.

## Configuration Parameters

### PagerDuty Configuration

- **routing_key**: The routing key to use.
- **create_description**: Whether to create a description instead of an issue.

## Example Configuration

```yaml
routing_key: your_routing_key
create_description: true
```
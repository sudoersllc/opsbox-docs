# Pagerduty Output Plugin

## Overview

The PagerDutyOutput Plugin processes and sends results to PagerDuty, allowing for incident creation and management based on the findings.

*This output plugin can be used by adding `pagerduty_out` to your pipeline.*

!!! note "Installation Package Name"

    `opsbox-pagerduty-output` is the name of this package.

    To use it, add `opsbox-pagerduty-output` to your project.

## Features

- **PagerDuty Integration**: Sends results to PagerDuty.
- **Customizable Incident Creation**: Allows specifying whether to create a description or an issue.

## Configuration Parameters

| Parameter          | Type | Description                                           | Required | Default |
|--------------------|------|-------------------------------------------------------|----------|---------|
| routing_key        | str  | The routing key to use.                               | Yes      | -       |
| create_description | bool | Whether to create a description instead of an issue.  | No       | False   |

***Description creation requires LLM***

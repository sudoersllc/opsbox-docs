# Plugin Documentation

This document provides an overview of the various plugins implemented for gathering and processing data, interacting with external services, and outputting results. The plugins are categorized into provider plugins for data gathering, assistant plugins for interacting with external services, and output plugins for processing and displaying results.

## Table of Contents

### Provider Plugins

- [EC2Provider](#ec2provider)
- [ELBProvider](#elbprovider)
- [RDSProvider](#rdsprovider)
- [S3Provider](#s3provider)
- [IAMProvider](#iamprovider)
- [Route53Provider](#route53provider)
- [CloudWatchProvider](#cloudwatchprovider)

### Assistant Plugins

- [Cost Savings](#cost-savings)
- [Lower Cost](#lower-cost)

### Output Plugins

- [JiraOutput](#jiraoutput)
- [EmailOutput](#emailoutput)
- [SlackOutput](#slackoutput)
- [CLIOutput](#clioutput)
- [TextFileOutput](#textfileoutput)
- [GithubOutput](#githuboutput)
- [AzureOutput](#azureoutput)
- [PagerDutyOutput](#pagerdutyoutput)
- [JSONOutput](#jsonoutput)

### Rego Plugins

- [Rego Checks](#checks)

---

## EC2Provider

### Overview

The EC2Provider plugin collects detailed information about AWS EC2 instances, including their associated volumes and Elastic IP addresses, to facilitate monitoring and management.

### Required Fields

```python
    aws_access_key_id: Annotated[str, Field(..., description="AWS access key ID", required=True)]
    aws_secret_access_key: Annotated[str, Field(..., description="AWS secret access key", required=True)]
    aws_region: Annotated[str |  None, Field(description="AWS region", required=False,default=None)]
    volume_tags: Annotated[
        str | None, Field(description="Key-value tag pairs for volumes", required=False, default=None)
    ]
    instance_tags: Annotated[
        str | None, Field(description="Key-value tag pairs for instances", required=False, default=None)
    ]
    eip_tags: Annotated[
        str | None, Field(description="Key-value tag pairs for Elastic IPs", required=False, default=None)
    ]


```

### Related Checks

- [IdleInstances](#idle_instances)
- [StrayEbs](#stray_ebs)

---

## ELBProvider

### Overview

The ELBProvider plugin gathers comprehensive data about AWS Elastic Load Balancers, including Classic, Application, and Network Load Balancers, to optimize performance and identify potential issues.

### Required Fields

```python
    aws_access_key_id: Annotated[str,Field(..., description="AWS access key ID", required=True)]
    aws_secret_access_key: Annotated[str,Field(..., description="AWS secret access key", required=True)]
    aws_region: Annotated[
        str | None, Field(description="AWS-Region", required=False, default=None)
    ]

```

### Related Checks

- [HighErrorRate](#high_error_rate)
- [InactiveLoadBalancers](#inactive_load_balancers)
- [LowRequestCount](#low_request_count)

---

## RDSProvider

### Overview

The RDSProvider plugin collects information about AWS RDS instances to help manage and optimize database performance and cost.

### Required Fields

```python
    aws_access_key_id: Annotated[str,Field(..., description="AWS access key ID", required=True)]
    aws_secret_access_key: Annotated[str,Field(..., description="AWS secret access key", required=True)]
    aws_region: Annotated[
        str | None, Field(description="AWS-Region", required=False, default=None)
    ]
```

### Related Checks

- [EmptyStorage](#empty_storage)
- [RDSIdle](#rds_idle)
- [ScalingDown](#scaling_down)

---

## S3Provider

### Overview

The S3Provider plugin gathers data related to AWS S3, including information about buckets, objects, and storage classes, to assist in storage management and cost optimization.

### Required Fields

```python
    aws_access_key_id: Annotated[str,Field(..., description="AWS access key ID", required=True)]
    aws_secret_access_key: Annotated[str,Field(..., description="AWS secret access key", required=True)]
    aws_region: Annotated[
        str | None, Field(description="AWS-Region", required=False, default=None)
    ]
```

### Related Checks

- [ObjectLastModified](#object_last_modified)
- [StorageClassUsage](#storage_class_usage)
- [UnusedBuckets](#unused_buckets)

---

## IAMProvider

### Overview

The IAMProvider plugin collects data related to AWS IAM, including information about users, groups, and roles, to help manage access and permissions effectively.

### Required Fields

```python
   aws_access_key_id: Annotated[str | None, Field(description="AWS access key ID", required=False,default=None)]
    aws_secret_access_key: Annotated[str | None, Field(description="AWS secret access key", required=False,default=None)]
    aws_region: Annotated[str | None, Field(description="AWS region", required=False, default=None)]
```

### Related Checks

- [Console_Acess](#console_access)
- [mfa_enabled](#mfa_enabled)
- [overdue_api_keys](#overdue_api_keys)
- [usued_policy](#unused_policy)

---

## Route53Provider

### Overview

The Route53Provider plugin collects data related to AWS Route53, including information about hosted zones, records, and health checks, to help manage DNS and routing effectively.

### Required Fields

```python
    aws_access_key_id: Annotated[str, Field(..., description="AWS access key ID", required=True)]
    aws_secret_access_key: Annotated[str, Field(..., description="AWS secret access key", required=True)]
    aws_region: Annotated[str | None, Field(description="AWS region", required=False, default=None)]
```

### Related Checks

- [empty_zones](#empty_zones)

---

## CloudWatchProvider

### Overview

The CloudWatchProvider plugin collects data related to AWS CloudWatch, including metrics and alarms, to help monitor and manage AWS resources effectively.

### Required Fields

```python
   aws_access_key_id: str = Field(..., description="AWS access key ID")
    aws_secret_access_key: str = Field(..., description="AWS secret access key")
    aws_region: str = Field(..., description="AWS region")
```

### Related Checks

- [cw_insights](#cw_insights)

## Cost Savings

### Overview

The Cost Savings plugin leverages large language models (LLMs) to generate recommendations for reducing cloud infrastructure costs based on the latest pipeline analysis.

**Module**: `cost_savings`

### Used Fields

```python
    arrigator: bool = Field(..., description="Whether to aggregate the data and generate one response.")
    discard_prior: bool = Field(
        False, description="Whether to discard the data before and leave only cost saving data."
    )

```

A Claude key or OpenAI key is required for generating content:

```python
claude_key: Annotated[str | None, Field(description="The Claude API key used for generating email content.", required=False, default=None)]
oai_key: Annotated[str | None, Field(description="The OpenAI API key used for generating email content.", required=False, default=None)]
```

---

## Lower Cost

### Overview

A plugin to generate recommendations for lowering costs on AWS EC2 instances.

**Module**: `lower_cost`

### Used Fields

```python
    aws_access_key_id: str = Field(..., description="AWS access key ID")
    aws_secret_access_key: str = Field(..., description="AWS secret access key")
    aws_region: str = Field(..., description="AWS region")
```

---

## JiraOutput

### Overview

The JiraOutput plugin creates and manages Jira issues based on check results, enabling effective tracking and resolution of identified problems.

**Module**: `jira_out`

### Required Fields

```python
jira_url: Annotated[str, Field(description="The URL of the Jira instance for issue creation.", required=True)]
jira_email: Annotated[str, Field(description="The email address used for authenticating to Jira.", required=True)]
jira_api_token: Annotated[str, Field(description="The API token used for authenticating to Jira.", required=True)]
jira_project_key: Annotated[str, Field(description="The key of the Jira project where issues will be created.", required=True)]
```

Currently, only OpenAI is supported for Jira:

```python
oai_key: Annotated[str, Field(description="The OpenAI API key used to assist with issue creation.", required=True)]
```

---

## EmailOutput

### Overview

The EmailOutput plugin sends out email notifications based on check results, ensuring that relevant stakeholders are informed in a timely manner.

**Module**: `email_out`

### Required Fields

```python
smtp_username: Annotated[str, Field(description="The username for SMTP server authentication.", required=True)]
smtp_password: Annotated[str, Field(description="The password for SMTP server authentication.", required=True)]
smtp_server: Annotated[str, Field(description="The SMTP server used for sending emails.", required=True)]
smtp_port: Annotated[str, Field(description="The port used for connecting to the SMTP server.", required=True)]
receiver_email_list: Annotated[str, Field(description="A comma-separated list of recipient email addresses.", required=True)]
```

A Claude key or OpenAI key is required for generating content:

```python
claude_key: Annotated[str | None, Field(description="The Claude API key used for generating email content.", required=False, default=None)]
oai_key: Annotated[str | None, Field(description="The OpenAI API key used for generating email content.", required=False, default=None)]
```

---

## SlackOutput

### Overview

The SlackOutput plugin sends messages to specified Slack channels based on pipeline outputs, providing real-time alerts to relevant teams.

**Module**: `slack_out`

### Required Fields

```python
slack_token: Annotated[str, Field(description="The Slack token used for authentication.", required=True)]
slack_channel: Annotated[str, Field(description="The Slack channel where the message will be posted.", required=True)]
```

---

## CLIOutput

### Overview

The CLIOutput plugin displays results directly in the command line interface, providing quick and accessible feedback.

**Module**: `cli_out`

---

## TextFileOutput

### Overview

The TextFileOutput plugin writes output results to a text file for record-keeping and further analysis.

**Module**: `text_out`

### Required Fields

```python
output_folder: Annotated[str | None, Field(description="The folder to output the results to.", required=False, default=None)]
```

---

## GithubOutput

### Overview

The GithubOutput plugin creates GitHub issues based on pipeline outputs, helping track and manage tasks or problems identified during analysis.

**Module**: `github_out`

### Required Fields

```python
github_token: Annotated[str, Field(description="The token for authenticating the GitHub user.", required=True)]
repo_owner: Annotated[str, Field(description="The owner of the repository where the issue will be created.", required=True)]
repo_name: Annotated[str, Field(description="The name of the repository where the issue will be created.", required=True)]
labels: Annotated[str | None, Field(description="Labels to apply to the created issue.", required=False, default=None)]
create_description: Annotated[bool, Field(description="Indicates whether to create a detailed description instead of an issue.", required=False, default=False)]
```

A Claude key or Open AI Keys are required if you have create_description set to true

```python
claude_key: Annotated[str | None,Field(description="The Claude API key to use.", required=False, default=None)]
```

```python
oai_key: Annotated[str | None, Field(description="The OpenAI API key to use.", required=False, default=None)]
```

---

## AzureOutput

### Overview

The AzureOutput plugin creates and manages Azure DevOps work items based on pipeline outputs, facilitating effective issue tracking and resolution.

**Module**: `azure_out`

### Required Fields

```python
azure_devops_token: Annotated[str, Field(description="The personal access token for authenticating with Azure DevOps.", required=True)]
azure_devops_organization: Annotated[str, Field(description="The name of the Azure DevOps organization.", required=True)]
azure_devops_project: Annotated[str, Field(description="The name of the Azure DevOps project.", required=True)]
azure_devops_username: Annotated[str, Field(description="The username used for authenticating with Azure DevOps.", required=True)]
azure_devops_priority: Annotated[int, Field(description="The priority level for the work item.", required=False, default=4)]
tags: Annotated[str | None, Field(description="Tags to apply to the work item.", required=False, default=None)]
create_description: Annotated[bool, Field(description="Indicates whether to create a detailed description instead of an issue.", required=False, default=False)]
```

A Claude key or Open AI Keys are required if you have create_description set to true

```python
    claude_key: Annotated[str | None,Field(description="The Claude API key to use.", required=False, default=None)]
```

```python
    oai_key: Annotated[str | None, Field(description="The OpenAI API key to use.", required=False, default=None)]
```

---

## PagerDutyOutput

### Overview

The PagerDutyOutput plugin sends alerts to PagerDuty based on pipeline outputs, ensuring prompt incident response and management.

**Module**: `pagerduty_out`

### Required Fields

```python
    routing_key: Annotated[str, Field(description="The routing_key to use.", required=True)]
    create_description: Annotated[bool,
    Field(description="Whether to create a description instead of an issue.", required=False, default=False)]
```

A Claude key or Open AI Keys are required if you have create_description set to true

```python
    claude_key: Annotated[str | None,Field(description="The Claude API key to use.", required=False, default=None)]
```

```python
    oai_key: Annotated[str | None, Field(description="The OpenAI API key to use.", required=False, default=None)]
```

---

## JSONOutput

### Overview

The JSONOutput plugin writes output results to a JSON file for further processing and analysis.

**Module**: `json_out`

### Required Fields

```python
          output_folder: Annotated[ str | None, Field(default="./findings/", description="The folder to output the results to.", required=False) ]
```

---

## Checks

### idle_instances

#### Overview

Checks for EC2 instances that are idle, determined by low CPU utilization.

#### Details

- **Module**: `idle_instances`
- **Rego File**: `idle_instances.rego`
- **Gather From**: [`EC2`](#ec2provider)

### stray_ebs

#### Overview

Identifies EBS volumes that are not in use.

#### Details

- **Module**: `stray_ebs`
- **Rego File**: `stray_ebs.rego`
- **Gather From**: [`EC2`](#ec2provider)

### high_error_rate

#### Overview

Checks for ELBs with high error rates.

#### Details

- **Module**: `high_error_rate`
- **Rego File**: `high_error_rate.rego`
- **Gather From**: [`ELB`](#elbprovider)

### inactive_load_balancers

#### Overview

Identifies underutilized ELBs based on request counts.

#### Details

- **Module**: `inactive_load_balancers`
- **Rego File**: `inactive_load_balancers.rego`
- **Gather From**: [`ELB`](#elbprovider)

### no_healthy_targets

#### Overview

Identifies ELBs with no healthy targets.

#### Details

- **Module**: `no_healthy_targets`
- **Rego File**: `no_healthy_targets.rego`
- **Gather From**: [`ELB`](#elbprovider)

### low_request_count

#### Overview

Identifies ELBs with low request counts.

#### Details

- **Module**: `low_request_count`
- **Rego File**: `low_request_count.rego`
- **Gather From**: [`ELB`](#elbprovider)

### empty_storage

#### Overview

Checks for RDS instances with low storage utilization.

#### Details

- **Module**: `empty_storage`
- **Rego File**: `empty_storage.rego`
- **Gather From**: [`RDS`](#rdsprovider)

### rds_idle

#### Overview

Identifies underutilized RDS instances with low CPU utilization and connections.

#### Details

- **Module**: `rds_idle`
- **Rego File**: `rds_idle.rego`
- **Gather From**: [`RDS`](#rdsprovider)

#### Overview

Provides recommendations for scaling down RDS instances based on low CPU utilization.

#### Details

- **Module**: `scaling_down`
- **Rego File**: `scaling_down.rego`
- **Gather From**: [`RDS`](#rdsprovider)

### object_last_modified

#### Overview

Identifies inactive S3 objects that haven't been modified in over 90 days.

#### Details

- **Module**: `object_last_modified`
- **Rego File**: `object_last_modified.rego`
- **Gather From**: [`S3`](#s3provider)

### storage_class_usage

#### Overview

Checks the usage of different storage classes in S3 buckets.

#### Details

- **Module**: `storage_class_usage`
- **Rego File**: `storage_class_usage.rego`
- **Gather From**: [`S3`](#s3provider)

### unused_buckets

#### Overview

Identifies unused S3 buckets based on their last modified time.

#### Details

- **Module**: `unused_buckets`
- **Rego File**: `unused_buckets.rego`
- **Gather From**: [`S3`](#s3provider)

### console_access

#### Overview

Identifies users with console access.

#### Details

- **Module**: `console_access`
- **Rego File**: `console_access.rego`
- **Gather From**: [`IAM`](#iamprovider)

### mfa_enabled

#### Overview

Identifies users with MFA disabled.

#### Details

- **Module**: `mfa_enabled`
- **Rego File**: `mfa_enabled.rego`
- **Gather From**: [`IAM`](#iamprovider)

### overdue_api_keys

#### Overview

Identifies API keys that are overdue for rotation.

#### Details

- **Module**: `overdue_api_keys`
- **Rego File**: `overdue_api_keys.rego`
- **Gather From**: [`IAM`](#iamprovider)

### unused_policy

#### Overview

Identifies unused policies in IAM.

#### Details

- **Module**: `unused_policy`
- **Rego File**: `unused_policy.rego`
- **Gather From**: [`IAM`](#iamprovider)

### empty_zones

#### Overview

Identifies empty hosted zones in Route53.

#### Details

- **Module**: `empty_zones`
- **Rego File**: `empty_zones.rego`
- **Gather From**: [`Route53`](#route53provider)

### cw_insights

#### Overview

provideds Cloudwatch metrics from boto3.

#### Details

- **Module**: `cw_insights`
- **Rego File**: `cw_insights.rego`
- **Gather From**: [`CloudWatch`](#cloudwatchprovider)

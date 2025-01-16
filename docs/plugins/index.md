# Opsbox Plugins
Welcome to the Opsbox plugins directory. This repository contains a collection of plugins designed to extend the functionality of Opsbox. Each plugin is defined in its own `pyproject.toml` file, which specifies the dependencies required for that plugin.

## Installing Plugins
### Through PyPI

This document outlines how to install Opsbox **[checks](#1-checks)** (for different services) and **[outputs](#2-outputs)** (for various integrations). 

---

## 1. Checks

Opsbox checks let you verify and monitor specific AWS services such as S3, RDS, ELB, EC2, etc. When you install the checks, Opsbox will also install the provider for the service.

### Installation

- **Using pip**:
  ```bash
  pip install opsbox-<service_name>-checks
  ```

- **Using uv**:
  ```bash
  uv add opsbox-<service_name>-checks
  ```

### Examples
- **Installing S3 checks (pip)**:
  ```bash
  pip install opsbox-s3-checks
  ```

- **Installing ELB checks (uv)**:
  ```bash
  uv add opsbox-elb-checks
  ```

- **Installing Route 53 checks (pip)**:
  ```bash
  pip install opsbox-r53-checks
  ```
  Note: Even though the service is called Route 53, use r53 in the package name.

## 2. Outputs
Opsbox outputs allow you to send results to various destinations—Slack, PagerDuty, GitHub, Azure DevOps, etc.

### Installation
- **Using pip**:
  ```bash
  pip install opsbox-<output_name>-output
  ```

- **Using uv**:
  ```bash
  uv add opsbox-<output_name>-output
  ```

### Examples
- **Installing Slack output (pip)**:
  ```bash
  pip install opsbox-slack-output
  ```

- **Installing Email output (uv)**:
  ```bash
  uv add opsbox-email-output
  ```

- **Installing JSON file output (pip)**:
  ```bash
  pip install opsbox-json-file-output
  ```

## Available Plugins

### Available Services
- AWS services:
    - [s3](/plugins/s3/s3_provider/s3_provider/)
    - [rds](/plugins/rds/rds_provider/rds_provider/)
    - [elb](/plugins/elb/elb_provider/elb_provider/)
    - [ec2](/plugins/ec2/ec2_provider/ec2_provider/)
    - [iam](/plugins/iam/iam_provider/iam_provider/)
    - [route53](/plugins/r53/r53_provider/r53_provider/)

### Available Outputs

- [azure](/plugins/outputs/azure/)
- [github](/plugins/outputs/github/)
- [cli](/plugins/outputs/cli/)
- [text-file](/plugins/outputs/text/)
- [json-file](/plugins/outputs/json/)
- [email](/plugins/outputs/email/)
- [jira](/plugins/outputs/jira/)
- [pagerduty](/plugins/outputs/pagerduty/)
- [slack](/plugins/outputs/slack/)

## Local Build

1. *Sync UV environment*
2. *Run build.py*
3. *Enjoy dists!*

### Sync UV environment
To begin, we first need to have a good testing/build environment.

In the root of the git directory, run `uv sync`. This will install everything needed.

### Run build.py
Next, run the bulk build script using `uv run build.py`

### Enjoy!
The build script will copy all the distributions to the root /dist folder.

Enjoy your distributions!

## Plugin Types

This repository contains various types of plugins, each serving a different purpose within Opsbox:

- **Assistants**: These plugins provide recommendations and strategies based on gathered data.
- **AWS Plugins**: These plugins offer checks and functionalities specific to AWS services.
- **Handlers**: These plugins handle various types of operations within Opsbox.
- **Outputs**: These plugins define different output formats for Opsbox results.

## Using Plugins with Opsbox

### Packages
Packages are autodetected by opsbox if they are in the same environment.

### Individual Modules
Once you have installed the necessary dependencies for the plugins in OpsBox's , you can point the main Opsbox program to this directory using the `--plugin_dir` option. Ensure you have installed the prerequisites for Opsbox before proceeding.

```sh
main.py ... --plugin_dir path/to/this/repository
```

This will allow Opsbox to load and utilize the plugins contained in this directory.

## Conclusion

This directory provides a comprehensive set of plugins to enhance the capabilities of Opsbox. By following the installation instructions and pointing Opsbox to this directory, you can leverage these plugins to optimize your operations.

For more information, refer to the individual plugin documentation and the Opsbox main documentation.
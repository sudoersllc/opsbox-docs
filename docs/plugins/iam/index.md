# Opsbox IAM Check Collection

Opsbox has a collection of rego checks to monitor various aspects of your IAM environment.

| Check Name                        | Description                                                        | Pipeline Name          |
|-----------------------------------|--------------------------------------------------------------------|------------------------|
| [Overdue API Keys](./overdue_api_keys.md) | Identifies IAM API keys that are overdue.                           | `overdue_api_keys`     |
| [IAM Users Without MFA](./mfa_enabled.md) | Identifies IAM users who do not have Multi-Factor Authentication (MFA) enabled. | `mfa_enabled`          |
| [Unused IAM Policies](./unused_policies.md) | Identifies IAM policies with zero attachments.                      | `unused_policies`      |
| [Console Access IAM](./console_access.md) | Identifies IAM users with console access enabled.                   | `console_access`       |

!!! note "Installation Collection Package Name"

    `opsbox-aws-iam-checks` is the name of this collection.

    To install any of the IAM checks in this collection, install this collection by adding `opsbox-aws-iam-checks` to your project.

    *These checks rely on the IAM Provider, which is installed as a prerequisite of this package.*
    *More info on the IAM provider can be found [here](./iam_provider/iam_provider.md)*

You can find more details about each check in their respective documentation files.
# Opsbox EC2 Check Collection

Opsbox has a collection of rego checks to monitor various aspects of your EC2 environment.

| Check Name        | Description                                                        |  Pipeline Name       |
|-------------------|--------------------------------------------------------------------|----------------------------|
| [Idle Instances](./idle_instances.md)    | Identifies EC2 instances with low utilization.                     | `idle_instances` |
| [Stray EBS Volumes](./stray_ebs.md) | Identifies EBS volumes not attached to any instances.              | `stray_ebs` |
| [Old EC2 Snapshots](./ec2_old_snapshots.md) | Identifies EC2 snapshots older than a specified period.            | `ec2_old_snapshots` |
| [Unattached EIPs](./unattached_eips.md)   | Identifies Elastic IPs not associated with any running instances.  | `unnattached_eips` |

!!! note "Installation Collection Package Name"

    `opsbox-ec2-checks` is the name of this collection.

    To install any of the EC2 checks in this collection, install this collection by adding `opsbox-ec2-checks` to your project.

    *These checks rely on the EC2 Provider, which is installed as a prerequisite of this package.*
    *More info on the EC2 provider can be found [here](./ec2_provider/ec2_provider.md)*

You can find more details about each check in their respective documentation files.

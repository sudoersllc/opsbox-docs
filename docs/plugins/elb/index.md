# Opsbox ELB Check Collection

Opsbox has a collection of rego checks to monitor various aspects of your ELB environment.

| Check Name                        | Description                                                        | Pipeline Name          |
|-----------------------------------|--------------------------------------------------------------------|------------------------|
| [Low Request Count](./low_request_counts.md) | Identifies load balancers with low request counts.                   | `low_request_counts`   |
| [No Healthy Targets](./no_healthy_targets.md) | Identifies load balancers where all targets are unhealthy.           | `no_healthy_targets`   |
| [High Error Rate](./high_error_rate.md) | Identifies load balancers with a high error rate.                    | `high_error_rate`      |
| [Inactive Load Balancers](./inactive_load_balancers.md) | Identifies load balancers that are inactive.                          | `inactive_load_balancers` |

!!! note "Installation Collection Package Name"

    `opsbox-elb-checks` is the name of this collection.

    To install any of the ELB checks in this collection, install this collection by adding `opsbox-elb-checks` to your project.

    *These checks rely on the ELB Provider, which is installed as a prerequisite of this package.*
    *More info on the ELB provider can be found [here](./elb_provider/elb_provider.md)*

You can find more details about each check in their respective documentation files.
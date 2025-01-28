# Opsbox Route 53 Check Collection

Opsbox has a collection of rego checks to monitor various aspects of your Route 53 environment.

| Check Name                        | Description                                                        | Pipeline Name          |
|-----------------------------------|--------------------------------------------------------------------|------------------------|
| [Empty Zones](./empty_zones.md)   | Identifies Route 53 hosted zones with no records.                  | `empty_zones`          |

!!! note "Installation Collection Package Name"

    `opsbox-r53-checks` is the name of this collection.

    To install any of the Route 53 checks in this collection, install this collection by adding `opsbox-r53-checks` to your project in either UV or pip.

    *These checks rely on the Route 53 Provider, which is installed as a prerequisite of this package.*
    *More info on the Route 53 provider can be found [here](./r53_provider/r53_provider.md)*

You can find more details about each check in their respective documentation files.
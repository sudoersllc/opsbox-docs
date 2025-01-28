# Opsbox RDS Check Collection

Opsbox has a collection of rego checks to monitor various aspects of your RDS environment.

| Check Name                        | Description                                                        | Pipeline Name          |
|-----------------------------------|--------------------------------------------------------------------|------------------------|
| [Empty Storage](./empty_storage.md) | Identifies RDS instances with empty storage.                        | `empty_storage`        |
| [RDS Idle](./rds_idle.md)         | Identifies idle RDS instances.                                      | `rds_idle`             |
| [Scaling Down](./scaling_down.md) | Identifies RDS instances that can be scaled down.                   | `scaling_down`         |
| [Old Snapshots](./old_snapshots.md) | Identifies old RDS snapshots that are no longer needed.             | `rds_old_snapshots`        |

!!! note "Installation Collection Package Name"

    `opsbox-rds-checks` is the name of this collection.

    To install any of the RDS checks in this collection, install this collection by adding `opsbox-rds-checks` to your project.

    *These checks rely on the RDS Provider, which is installed as a prerequisite of this package.*
    *More info on the RDS provider can be found [here](./rds_provider/rds_provider.md)*

You can find more details about each check in their respective documentation files.
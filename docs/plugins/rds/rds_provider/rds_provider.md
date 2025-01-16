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

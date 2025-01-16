## ELBProvider

### Overview
The ELBProvider plugin gathers comprehensive data about AWS Elastic Load Balancers, including Classic, Application, and Network Load Balancers, to optimize performance and identify potential issues.

### Commands to install the plugin
to install the plugin individually use the following command
```bash
uv add opsbox-elb-provider
```
to install the plugin as part of the AWS bundle use the following command
```bash
uv add "opsbox[aws]"
```



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
- [no_helathy_targets](#no_healthy_target)


## Route53Provider

### Overview
The Route53Provider plugin collects data related to AWS Route53, including information about hosted zones, records, and health checks, to help manage DNS and routing effectively.

### Commands to install the plugin
to install the plugin individually use the following command
```bash
uv add opsbox-r53-provider
```
to install the plugin as part of the AWS bundle use the following command
```bash
uv add "opsbox[aws]"
```
### Required Fields
```python
    aws_access_key_id: Annotated[str, Field(..., description="AWS access key ID", required=True)]
    aws_secret_access_key: Annotated[str, Field(..., description="AWS secret access key", required=True)]
    aws_region: Annotated[str | None, Field(description="AWS region", required=False, default=None)]
```

### Related Checks
- [empty_zones](#empty_zones)



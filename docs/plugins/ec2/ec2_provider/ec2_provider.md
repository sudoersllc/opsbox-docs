# EC2Provider

### Overview
The EC2Provider plugin collects detailed information about AWS EC2 instances, including their associated volumes and Elastic IP addresses, to facilitate monitoring and management.

### Commands to install the plugin
to install the plugin individually use the following command
```bash
uv add opsbox-ec2-provider
```
to install the plugin as part of the AWS bundle use the following command
```bash
uv add "opsbox[aws]"
```

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

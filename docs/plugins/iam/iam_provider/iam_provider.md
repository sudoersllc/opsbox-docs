## IAMProvider

### Overview
The IAMProvider plugin collects data related to AWS IAM, including information about users, groups, and roles, to help manage access and permissions effectively.

### Commands to install the plugin
to install the plugin individually use the following command
```bash
uv add opsbox-iam-provider
```
to install the plugin as part of the AWS bundle use the following command
```bash
uv add "opsbox[aws]"
```

### Required Fields
```python
   aws_access_key_id: Annotated[str | None, Field(description="AWS access key ID", required=False,default=None)]
    aws_secret_access_key: Annotated[str | None, Field(description="AWS secret access key", required=False,default=None)]
    aws_region: Annotated[str | None, Field(description="AWS region", required=False, default=None)]
```

### Related Checks
- [Console_Acess](#console_access)
- [mfa_enabled](#mfa_enabled)
- [overdue_api_keys](#overdue_api_keys)
- [usued_policy](#unused_policy)

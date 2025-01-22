
## S3Provider

### Overview
The S3Provider plugin gathers data related to AWS S3, including information about buckets, objects, and storage classes, to assist in storage management and cost optimization.

### Required Fields
```python
    aws_access_key_id: Annotated[str,Field(..., description="AWS access key ID", required=True)]
    aws_secret_access_key: Annotated[str,Field(..., description="AWS secret access key", required=True)]
    aws_region: Annotated[
        str | None, Field(description="AWS-Region", required=False, default=None)
    ]
```

### Related Checks
- [ObjectLastModified](#object_last_modified)
- [StorageClassUsage](#storage_class_usage)
- [UnusedBuckets](#unused_buckets)


---
{
"title": "S3 Load",
"language": "en"
}
---

# S3 Load

Starting from version 0.14, Doris supports the direct import of data from online storage systems that support the S3 protocol through the S3 protocol.

This document mainly introduces how to import data stored in AWS S3. It also supports the import of other object storage systems that support the S3 protocol, such as Baidu Cloud’s BOS, Alibaba Cloud’s OSS and Tencent Cloud’s COS, etc.

## Applicable scenarios

- Source data in S3 protocol accessible storage systems, such as S3, BOS.
- Data volumes range from tens to hundreds of GB.

## Preparing

1. Standard AK and SK First, you need to find or regenerate AWS `Access keys`, you can find the generation method in `My Security Credentials` of AWS console, as shown in the following figure: [AK_SK](https://doris.apache.org/images/aws_ak_sk.png) Select `Create New Access Key` and pay attention to save and generate AK and SK.
2. Prepare REGION and ENDPOINT REGION can be selected when creating the bucket or can be viewed in the bucket list. ENDPOINT can be found through REGION on the following page [AWS Documentation](https://docs.aws.amazon.com/general/latest/gr/s3.html#s3_region)

Other cloud storage systems can find relevant information compatible with S3 in corresponding documents

## Start Loading

Like Broker Load just replace `WITH BROKER broker_name ()` with

```text
    WITH S3
    (
        "AWS_ENDPOINT" = "AWS_ENDPOINT",
        "AWS_ACCESS_KEY" = "AWS_ACCESS_KEY",
        "AWS_SECRET_KEY"="AWS_SECRET_KEY",
        "AWS_REGION" = "AWS_REGION"
    )
```

example:

```sql
    LOAD LABEL example_db.example_label_1
    (
        DATA INFILE("s3://your_bucket_name/your_file.txt")
        INTO TABLE load_test
        COLUMNS TERMINATED BY ","
    )
    WITH S3
    (
        "AWS_ENDPOINT" = "AWS_ENDPOINT",
        "AWS_ACCESS_KEY" = "AWS_ACCESS_KEY",
        "AWS_SECRET_KEY"="AWS_SECRET_KEY",
        "AWS_REGION" = "AWS_REGION"
    )
    PROPERTIES
    (
        "timeout" = "3600"
    );
```

## FAQ

1. S3 SDK uses virtual-hosted style by default. However, some object storage systems may not be enabled or support virtual-hosted style access. At this time, we can add the `use_path_style` parameter to force the use of path style:

```text
   WITH S3
   (
         "AWS_ENDPOINT" = "AWS_ENDPOINT",
         "AWS_ACCESS_KEY" = "AWS_ACCESS_KEY",
         "AWS_SECRET_KEY"="AWS_SECRET_KEY",
         "AWS_REGION" = "AWS_REGION",
         "use_path_style" = "true"
   )
```

<version since="1.2">

2. Support using temporary security credentials to access object stores that support the S3 protocol:

```
  WITH S3
  (
        "AWS_ENDPOINT" = "AWS_ENDPOINT",
        "AWS_ACCESS_KEY" = "AWS_TEMP_ACCESS_KEY",
        "AWS_SECRET_KEY" = "AWS_TEMP_SECRET_KEY",
        "AWS_TOKEN" = "AWS_TEMP_TOKEN",
        "AWS_REGION" = "AWS_REGION"
  )
```

</version>

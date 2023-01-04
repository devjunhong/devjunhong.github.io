---
title: "Empty S3 bucket by command"
excerpt: "AWS console may not be your friend if you have bulk to delete"
toc: true
toc_sticky: true
published: true
layout: single
# classes: wide
word-wrap: break-word;
categories:
    - S3
    - AWS
    - tip
    - Shell Script
tags:
    - S3
    - AWS
    - tip
    - Shell script
last_modified_at: 2023-01-04T06:43:00-05:00
---

# What's the problem? 
To delete the S3 bucket, we need to make them empty. If the bucket holds tons of data, would you be waiting for jobs in the `AWS console`? From my experience, `AWS console` is freezing after a while. These command lines help you to take them out. Please be aware that this will create a file in your local. `aws s3api delete-objects` command will actually delete. 


# Solution 
This was successful with Mac OS. 

```sh
#!/bin/sh
BUCKET=here_is_your_s3_bucket_name

# List S3 keys and save to a file
aws s3api list-objects --output text --bucket ${BUCKET} --query 'Contents[].[Key]' | pv -l > BUCKET.keys

# Delete S3 keys from file
tail -n+0 BUCKET.keys | pv -l | grep -v -e "'" | tr '\n' '\0' | xargs -0 -P1 -n1000 bash -c 'aws s3api delete-objects --bucket ${BUCKET} --delete "Objects=[$(printf "{Key=%q}," "$@")],Quiet=true"' _
```
## Using ansible as policy as code.

- In this practice handson we are writting up ansible playbook which will look for S3 buckets present under aws acccount & fetch it's information. Not only that but also enable versioning on S3 bucket if it's disabled on any S3 bucket.

## Refrence Docs
- https://docs.ansible.com/ansible/latest/collections/amazon/aws/s3_bucket_module.html#ansible-collections-amazon-aws-s3-bucket-module
- https://docs.ansible.com/ansible/latest/collections/amazon/aws/s3_bucket_info_module.html#ansible-collections-amazon-aws-s3-bucket-info-module
- https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_environment.html
- https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_lookups.html
- https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html


🔁 Quick Rule of Thumb
| Use Case | Use | | Use - |
|----------------------------------|----------------------|-----------------------------|
| One multiline string | ✅ Yes | 🚫 No |
| Multiple independent messages | 🚫 No | ✅ Yes |
| Want newline preserved | ✅ Yes | 🚫 No (each is separate) |
| Output shown as YAML list | 🚫 No | ✅ Yes |

--- 

## Outcomes of this hands-on in the form of screenshots
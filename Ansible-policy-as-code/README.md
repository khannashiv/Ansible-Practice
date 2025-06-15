## Using ansible as policy as code.

- In this practice handson we are writting up ansible playbook which will look for S3 buckets present under aws acccount & fetch it's information. Not only that but also enable versioning on S3 bucket if it's disabled on any S3 bucket.

## Refrence Docs
- https://docs.ansible.com/ansible/latest/collections/amazon/aws/s3_bucket_module.html#ansible-collections-amazon-aws-s3-bucket-module
- https://docs.ansible.com/ansible/latest/collections/amazon/aws/s3_bucket_info_module.html#ansible-collections-amazon-aws-s3-bucket-info-module
- https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_environment.html
- https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_lookups.html
- https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html
- https://github.com/iam-veeramalla/ansible-zero-to-hero

## Command used

- (ansible-venv) ubuntu@LAPTOP-49SH4K4V:~/Ansible-Practice-1/Ansible-policy-as-code$ ansible-playbook pac.yaml

🔁 Quick Rule of Thumb
| Use Case | Use | | Use - |
|----------------------------------|----------------------|-----------------------------|
| One multiline string | ✅ Yes | 🚫 No |
| Multiple independent messages | 🚫 No | ✅ Yes |
| Want newline preserved | ✅ Yes | 🚫 No (each is separate) |
| Output shown as YAML list | 🚫 No | ✅ Yes |

--- 

## Outcomes of this hands-on in the form of screenshots

--- 

- ![Ansible-PAC-1](../Images/Ansible-PAC-1.png)
- ![Ansible-PAC-2](../Images/Ansible-PAC-2.png)
- ![Ansible-PAC-3](../Images/Ansible-PAC-3.png)
- ![Ansible-PAC-4](../Images/Ansible-PAC-4.png)
- ![Ansible-PAC-5](../Images/Ansible-PAC-5.png)
- ![Ansible-PAC-6](../Images/Ansible-PAC-6.png)
- ![Ansible-PAC-7](../Images/Ansible-PAC-7.png)

---
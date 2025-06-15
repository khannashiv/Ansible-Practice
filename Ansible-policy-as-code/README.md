# Using Ansible as Policy as Code

In this hands-on practice, we are writing an Ansible playbook that will:
- Discover S3 buckets present under an AWS account and fetch their information.
- Enable versioning on S3 buckets if not already enabled.

---

## Reference Docs

- [Ansible aws_s3_bucket Module](https://docs.ansible.com/ansible/latest/collections/amazon/aws/s3_bucket_module.html#ansible-collections-amazon-aws-s3-bucket-module)
- [Ansible aws_s3_bucket_info Module](https://docs.ansible.com/ansible/latest/collections/amazon/aws/s3_bucket_info_module.html#ansible-collections-amazon-aws-s3-bucket-info-module)
- [Ansible Playbook Guide: Environment](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_environment.html)
- [Ansible Playbook Guide: Lookups](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_lookups.html)
- [Ansible Playbook Guide: Loops](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html)
- [Ansible Zero to Hero (GitHub)](https://github.com/iam-veeramalla/ansible-zero-to-hero)

---

## Command Used

```bash
(ansible-venv) ubuntu@LAPTOP-49SH4K4V:~/Ansible-Practice-1/Ansible-policy-as-code$ ansible-playbook pac.yaml
```

---

## Quick Rule of Thumb

| Use Case                       | Use `|-` (Literal Block) | Use `|` (Folded Block)      |
|---------------------------------|:-----------------------:|:--------------------------:|
| One multiline string            |          ✅ Yes         |            🚫 No           |
| Multiple independent messages   |          🚫 No          |            ✅ Yes           |
| Want newline preserved          |          ✅ Yes         |            🚫 No           |
| Output shown as YAML list       |          🚫 No          |            ✅ Yes           |

---

## Outcomes of this Hands-On (Screenshots)

- ![Ansible-PAC-1](../Images/Ansible-PAC-1.png)
- ![Ansible-PAC-2](../Images/Ansible-PAC-2.png)
- ![Ansible-PAC-3](../Images/Ansible-PAC-3.png)
- ![Ansible-PAC-4](../Images/Ansible-PAC-4.png)
- ![Ansible-PAC-5](../Images/Ansible-PAC-5.png)
- ![Ansible-PAC-6](../Images/Ansible-PAC-6.png)
- ![Ansible-PAC-7](../Images/Ansible-PAC-7.png)

---
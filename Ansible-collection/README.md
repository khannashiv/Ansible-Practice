# Ansible EC2 Collection Setup & Authentication Guide

This guide will help you set up the required dependencies and securely manage AWS credentials for Ansible automation with EC2.

---

## 1. Install Dependencies

### Install `boto3`

```sh
pip install boto3
```

### Install AWS Ansible Collection

```sh
ansible-galaxy collection install amazon.aws
```

---

## 2. Secure AWS Credentials with Ansible Vault

### Step 1: Create a Vault Password File

```sh
openssl rand -base64 2048 > vault.pass
```

### Step 2: Add AWS Credentials to Vault

```sh
ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
```

Add your AWS credentials in the `pass.yml` file as needed.

---

**Tip:**  
Keep your `vault.pass` file secure and never commit it to version control.

## Reference Docs

- [Ansible Builtin Collection Plugins](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html#plugins-in-ansible-builtin)
- [Ansible Collections Documentation](https://docs.ansible.com/ansible/latest/collections/index.html)
- [Amazon AWS Collection for Ansible](https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_instance_module.html#ansible-collections-amazon-aws-ec2-instance-module)
- [Amazon AWS Collection on Ansible Galaxy](https://galaxy.ansible.com/ui/repo/published/amazon/aws/)

- [Playbook Variables Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html)
- [Ansible Vault CLI Documentation](https://docs.ansible.com/ansible/2.8/cli/ansible-vault.html#create)
- [Managing Multiple Vault Passwords](https://docs.ansible.com/ansible/2.8/user_guide/playbooks_vault.html#multiple-vault-passwords)

- [Ansible Lint Syntax Check Rules](https://ansible.readthedocs.io/projects/lint/rules/syntax-check/)
- [Ansible Lint YAML Rules](https://ansible.readthedocs.io/projects/lint/rules/yaml/)

## Common Ansible Commands used in this hands on.

### Run Playbook

```sh
ansible-playbook modified-ec2-create.yaml
```

### Run Playbook with Vault Password File

```sh
ansible-playbook modified-ec2-create.yaml --vault-password-file vault.pass
```

### Create Vault-Encrypted Variable File

```sh
ansible-vault create ec2-role/vars/main.yml --vault-password-file vault.pass
```

### Encrypt an Existing Variable File

```sh
ansible-vault encrypt ec2-role/vars/main.yml --vault-password-file vault.pass
```

### Decrypt a Variable File

```sh
ansible-vault decrypt ec2-role/vars/main.yml --vault-password-file vault.pass
```

### Edit a Vault-Encrypted Variable File

```sh
ansible-vault edit ec2-role/vars/main.yml --vault-password-file vault.pass
```

### Syntax Check a Playbook

```sh
ansible-playbook -i localhost, --syntax-check ./modified-ec2-create.yaml --vault-password-file vault.pass
```

### Run Playbook with Extra Variables

```sh
ansible-playbook modified-ec2-create.yaml --vault-password-file vault.pass -e ec2_instance_type=t2.medium
```

### Run Playbook with Extra Vars File

```sh
ansible-playbook modified-ec2-create.yaml --extra-vars "@vault-aws.yaml"
```
## Outcomes of Handson in the form of screenshots.

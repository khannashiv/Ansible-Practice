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
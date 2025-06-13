# 🚀 Ansible EC2 Collection Setup & Authentication Guide

Easily set up dependencies and securely manage AWS credentials for Ansible automation with EC2.

---

## 1️⃣ Install Dependencies

### Install `boto3`

```sh
pip install boto3
```

### Install AWS Ansible Collection

```sh
ansible-galaxy collection install amazon.aws
```

---

## 2️⃣ Secure AWS Credentials with Ansible Vault

### Step 1: Create a Vault Password File

```sh
openssl rand -base64 2048 > vault.pass
```

### Step 2: Add AWS Credentials to Vault

```sh
ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
```

Add your AWS credentials in the `pass.yml` file as needed.

> **⚠️ Keep your `vault.pass` file secure and never commit it to version control!**

---

## 📚 Reference Docs

- [Ansible Builtin Collection Plugins](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html#plugins-in-ansible-builtin)
- [Ansible Collections Documentation](https://docs.ansible.com/ansible/latest/collections/index.html)
- [Amazon AWS Collection for Ansible](https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_instance_module.html#ansible-collections-amazon-aws-ec2-instance-module)
- [Amazon AWS Collection on Ansible Galaxy](https://galaxy.ansible.com/ui/repo/published/amazon/aws/)
- [Playbook Variables Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html)
- [Ansible Vault CLI Documentation](https://docs.ansible.com/ansible/2.8/cli/ansible-vault.html#create)
- [Managing Multiple Vault Passwords](https://docs.ansible.com/ansible/2.8/user_guide/playbooks_vault.html#multiple-vault-passwords)
- [Ansible Lint Syntax Check Rules](https://ansible.readthedocs.io/projects/lint/rules/syntax-check/)
- [Ansible Lint YAML Rules](https://ansible.readthedocs.io/projects/lint/rules/yaml/)

---

## 🛠️ Common Ansible Commands

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

---

## 💡 Points to Note

You can provide AWS credentials in different ways:

### **Method 1:** Pass Encrypted Vars File at Runtime

Remove `vars_files` from your playbook and use:

```sh
ansible-playbook modified-ec2-create.yaml --extra-vars "@vault-aws.yaml" --vault-password-file vault.pass
```

### **Method 2:** Use Roles and Encrypted Vars

1. Move credentials from `vault-aws.yaml` to `ec2-role/vars/main.yml`.
2. Encrypt with:
    ```sh
    ansible-vault encrypt roles/ec2-role/vars/main.yml --vault-password-file vault.pass
    ```
3. Reference the role in your playbook:
    ```yaml
    ---
    - name: Launch EC2 via role
      hosts: localhost
      connection: local
      roles:
        - ec2-role
    ```
4. Run with:
    ```sh
    ansible-playbook modified-ec2-create.yaml --vault-password-file vault.pass
    ```

---

## 🔒 Example: Vault Encryption & Secure Commit Workflow

1. Write AWS credentials in `roles/ec2-role/vars/main.yml`.
2. Encrypt:
    ```sh
    ansible-vault encrypt roles/ec2-role/vars/main.yml --vault-password-file vault.pass
    ```
3. Add to `.gitignore`:
    ```
    ec2-role/vars/main.yml
    ```
4. Commit encrypted file:
    ```sh
    git add .
    git commit -m "Add encrypted AWS credentials to role"
    git push
    ```
5. Run playbook:
    ```sh
    ansible-playbook ec2-create.yaml --vault-password-file vault.pass
    ```

---

## ❓ FAQ: Using `@` with `--extra-vars`

- **Q:** Do we need the `@` symbol with `--extra-vars`?
- **A:** Yes! The `@` tells Ansible to load variables from a file.

    - Example:
        ```sh
        ansible-playbook playbook.yaml --extra-vars "@vault-aws.yaml"
        ```
    - Without `@`, provide inline key-value pairs:
        ```sh
        ansible-playbook playbook.yaml --extra-vars "aws_access_key_id=xyz aws_secret_access_key=abc"
        ```

- **Encrypted files:**  
  Use `--vault-password-file` with encrypted vars files:
    ```sh
    ansible-playbook playbook.yaml --extra-vars "@vault-aws.yaml" --vault-password-file vault.pass
    ```

---

## 📝 .gitignore & Sensitive Files

- `.gitignore` only prevents **untracked** files from being added.
- If a file is already tracked, stop tracking with:
    ```sh
    git rm --cached Ansible-collection/ec2-role/vars/main.yml
    git commit -m "Stop tracking main.yml file"
    git push origin main
    ```
- Add to `.gitignore`:
    ```
    ec2-role/vars/main.yml
    ```
- Check status:
    ```sh
    git status
    ```

---

## 📸 Outcomes of Hands-on (Screenshots)

_Add your screenshots here to document your results!_
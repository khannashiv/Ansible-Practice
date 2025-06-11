# Converting a Sample Ansible Playbook to a Role

This guide demonstrates how to convert a basic Ansible playbook into a reusable Ansible role.

---

## 1. Initial Directory Structure

Let's assume you start with the following minimal files on your Ansible controller:

```
(ansible-venv) root@LAPTOP-49SH4K4V:~# ls -al
-rw-r--r--  1 root   root   1985 Jun 11 13:18 index.html
-rw-r--r--  1 root   root     53 Jun 11 08:22 inventory.ini
-rw-r--r--  1 root   root    362 Jun 11 12:55 sample-playbook.yaml
```

---

## 2. Converting to a Role

Use the following command to initialize a new role named `apache2`:

```sh
ansible-galaxy init role apache2
```

This creates a directory structure like:

```
(ansible-venv) root@LAPTOP-49SH4K4V:~# ls -al
drwxr-xr-x  5 root   root   4096 Jun 11 05:36 ansible-venv
drwxr-xr-x 10 root   root   4096 Jun 11 14:05 apache2
-rw-r--r--  1 root   root     53 Jun 11 08:22 inventory.ini
-rw-r--r--  1 root   root     55 Jun 11 14:13 sample-playbook.yaml
```

Inside the role directory:

```
(ansible-venv) root@LAPTOP-49SH4K4V:~/apache2# ls -al
total 44
drwxr-xr-x 10 root root 4096 Jun 11 14:05 .
drwx------  7 root root 4096 Jun 11 14:16 ..
-rw-r--r--  1 root root 1328 Jun 11 14:05 README.md
drwxr-xr-x  2 root root 4096 Jun 11 14:05 defaults
drwxr-xr-x  2 root root 4096 Jun 11 14:14 files
drwxr-xr-x  2 root root 4096 Jun 11 14:05 handlers
drwxr-xr-x  2 root root 4096 Jun 11 14:05 meta
drwxr-xr-x  2 root root 4096 Jun 11 14:16 tasks
drwxr-xr-x  2 root root 4096 Jun 11 14:05 templates
drwxr-xr-x  2 root root 4096 Jun 11 14:05 tests
drwxr-xr-x  2 root root 4096 Jun 11 14:05 vars
```

---

## 3. Migrating the Playbook Tasks to Role

- Remove the `tasks` section from `sample-playbook.yaml`.
- Move the content under `tasks` to `apache2/tasks/main.yml`.

### Updated `sample-playbook.yaml`

```yaml
---
- hosts: all
  become: true
  roles:
    - apache2
```

### Updated `apache2/tasks/main.yml`

```yaml
# SPDX-License-Identifier: MIT-0
---
# Task files for apache2
- name: Install apache httpd
  ansible.builtin.apt:
    name: apache2
    state: present
    update_cache: yes

- name: Copy file with owner and permissions
  ansible.builtin.copy:
    src: files/index.html
    dest: /var/www/html
    owner: root
    group: root
    mode: '0644'
```

---

## 4. Moving Static Files

Move `index.html` from your home directory to `apache2/files/index.html` and update the path in `main.yml` as shown above.

---

## 5. Testing

- Manually remove `index.html` from `/var/www/html` on one of your EC2 instances to test the deployment.
- Run the updated `sample-playbook.yaml`. The playbook should execute successfully and copy `index.html` to the EC2 instance.

---
## Converting sample ansible playbook to role.

- Let say we have follwing directory structure on my ansible controller with bare minimum files as shown below.
- As we can see we have file in the following directory structure i.e. sample ansible playbook like shown below. Let's try to convert to ansible role.

(ansible-venv) root@LAPTOP-49SH4K4V:~# ls -al
-rw-r--r--  1 root   root   1985 Jun 11 13:18 index.html
-rw-r--r--  1 root   root     53 Jun 11 08:22 inventory.ini
-rw-r--r--  1 root   root    362 Jun 11 12:55 sample-playbook.yaml

- We are using command i.e. `ansible-galaxy init role apache2`. This will create a new directory structure like shown below.

(ansible-venv) root@LAPTOP-49SH4K4V:~# ls -al
drwxr-xr-x  5 root   root   4096 Jun 11 05:36 ansible-venv
drwxr-xr-x 10 root   root   4096 Jun 11 14:05 apache2
-rw-r--r--  1 root   root     53 Jun 11 08:22 inventory.ini
-rw-r--r--  1 root   root     55 Jun 11 14:13 sample-playbook.yaml

(ansible-venv) root@LAPTOP-49SH4K4V:~# cd apache2/
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

- Now the very first steps is we will remove tasks section from sample-playbook.yaml & add content under tasks section to main.yaml which is present under tasks folder in the above directory structure.

- Along with that we will have new sample-playbook.yaml & updated main.yml i.e. apache2/tasks/main.yml like shown below :

(ansible-venv) root@LAPTOP-49SH4K4V:~# ls
Jenkins-KVP.pem  Jenkins-KVP.pub  ansible-venv  apache2  inventory.ini  sample-playbook.yaml
(ansible-venv) root@LAPTOP-49SH4K4V:~# cat sample-playbook.yaml
---
- hosts: all
  become: true
  roles:
    - apache2


(ansible-venv) root@LAPTOP-49SH4K4V:~# cat apache2/tasks/main.yml
#SPDX-License-Identifier: MIT-0
---
#Task files for apache2
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
    mode: '0644'# tasks file for apache2
(ansible-venv) root@LAPTOP-49SH4K4V:~#

- We have also shifted index.html file from home directory to /apache2/files/index.html & updated the path under main.yaml present under tasks folder.

- From the testing standpoint we have amnaully removed index.html from one of the EC2 instance present under /var/ww/html directory.

- Finally we ran our updated sample-playbook.yaml which executed successfully updating EC2 instance with index.html file
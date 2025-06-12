# Ansible Galaxy Guide

## Reference Documentation

- [Ansible Galaxy UI](https://galaxy.ansible.com/ui/)
- [Ansible Galaxy User Guide](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html)
- [bsmeding.docker Role Documentation](https://galaxy.ansible.com/ui/standalone/roles/bsmeding/docker/documentation/)

---

## Sample Commands

```sh
ansible-galaxy -h
ansible-galaxy role -h
ansible-galaxy collection -h
ansible-galaxy role install bsmeding.docker
```

---

## Demo: Installing an Ansible Role from Galaxy

This demo shows how to install the `bsmeding.docker` role from Ansible Galaxy and use it to install Docker on managed nodes.

- The role supports installing Docker on different Linux distributions.
- [Role Install URL](https://galaxy.ansible.com/ui/standalone/roles/bsmeding/docker/install/)
- **Install command:**
  ```sh
  ansible-galaxy role install bsmeding.docker
  ```
- Roles are installed by default to:  
  `/root/.ansible/roles`
- To execute the role, use the provided playbook:  
  `docker-playbook.yaml` (which references the `bsmeding.docker` role) with the command as : `ansible-playbook -i inventory.ini docker-playbook.yaml`

  ## Publishing ansible custom role to ansible galaxy repository.
  
   - Ansible role should be first moved to github
   - from github we can import to ansible galaxy repository.
 
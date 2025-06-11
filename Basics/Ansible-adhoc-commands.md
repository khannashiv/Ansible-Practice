# Sample Ansible Adhoc Commands

## Reference Documentation

- [Ansible Adhoc Commands Guide](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html)

---

## Sample Commands Tested in LAB Setup

- **Run disk usage command on all hosts:**
  ```sh
  ansible -i inventory.ini -m shell -a "df -h" all
  ```

- **Ping all hosts to check connectivity:**
  ```sh
  ansible -i inventory.ini -m ping all
  ```

- **List all files in `/etc/` directory on the `app` group:**
  ```sh
  ansible -i inventory.ini -m shell -a "ls -al /etc/" app
  ```

- **Update packages and install OpenJDK 11 on all hosts:**
  ```sh
  ansible -i inventory.ini -m shell -a "sudo apt-get update && sudo apt-get install -y openjdk-11-jdk" all
  ```

---

## Outcomes of Sample Commands

- ![Ansible-adhoc-1](../Images/Ansible-adhoc-1.png)
- ![Ansible-adhoc-2](../Images/Ansible-adhoc-2.png)
- ![Ansible-adhoc-3](../Images/Ansible-adhoc-3.png)
- ![Ansible-adhoc-4](../Images/Ansible-adhoc-4.png)
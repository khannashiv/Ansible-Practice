## Installing and setting up Ansible.

**Refrence Docs**
- [Official Ansible Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible)
- This guide assumes you are using a Windows machine as the Ansible controller node.
- **Prerequisite:** Install Windows Subsystem for Linux (WSL). See [Microsoft WSL Install Guide](https://learn.microsoft.com/en-us/windows/wsl/install).
- After installing WSL, install Ubuntu from the Microsoft Store.
- **Tip:** Ensure your Ubuntu installation is up to date before proceeding.

### Setting up Ansible in a Python Virtual Environment

1. **Update package lists:**
    ```sh
    sudo apt update
    ```
2. **Install Python venv and pip:**
    ```sh
    sudo apt install python3-venv python3-pip -y
    ```
3. **Create a virtual environment for Ansible:**
    ```sh
    python3 -m venv ~/ansible-venv
    ```
4. **Activate the virtual environment:**
    ```sh
    source ~/ansible-venv/bin/activate
    ```
5. **Install Ansible:**
    ```sh
    pip install ansible
    ```

> **Note:** Each time you want to use Ansible, activate the environment:
> ```sh
> source ~/ansible-venv/bin/activate
> ```

---

**Additional Pointers:**
- Make sure you have enabled virtualization in your BIOS if you encounter issues with WSL.
- For persistent SSH connections to managed nodes, generate SSH keys and copy them to your target machines.
- Consider installing `ansible-lint` for best practices:
  ```sh
  pip install ansible-lint
  ```
- For more advanced usage, refer to the [Ansible User Guide](https://docs.ansible.com/ansible/latest/user_guide/index.html).
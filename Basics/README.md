# Installing and Setting Up Ansible

Welcome! This guide will walk you through installing and configuring Ansible on a Windows machine using Windows Subsystem for Linux (WSL).

---

## 📚 Reference Docs

- [Official Ansible Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible)
- [Microsoft WSL Install Guide](https://learn.microsoft.com/en-us/windows/wsl/install)

> **Prerequisite:**  
> Install **Windows Subsystem for Linux (WSL)** and then **Ubuntu** from the Microsoft Store.  
> **Tip:** Ensure your Ubuntu installation is up-to-date before proceeding.

---

## 🐍 Setting up Ansible in a Python Virtual Environment

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

> **Note:**  
> Every time you want to use Ansible, activate the environment:
> ```sh
> source ~/ansible-venv/bin/activate
> ```

---

## 💡 Additional Pointers

- Ensure virtualization is enabled in your BIOS if WSL has issues starting.
- For persistent SSH connections to managed nodes, generate SSH keys and copy them to your target machines.
- Install `ansible-lint` for best practices:
  ```sh
  pip install ansible-lint
  ```
- For more advanced usage, check the [Ansible User Guide](https://docs.ansible.com/ansible/latest/user_guide/index.html).

---

## 🔑 Setting up Passwordless SSH Authentication for Managed Nodes

To allow your Ansible control node to connect to managed nodes without entering a password each time, follow these steps:

1. **Copy your private key to your Linux home directory (if needed):**
   ```sh
   cp /mnt/d/path/to/your/private-key.pem ~/your-key.pem
   ```
   Replace `/mnt/d/path/to/your/private-key.pem` with the actual path to your private key file on your Windows machine, and `~/your-key.pem` with your Ubuntu path.

   For example:  
   ```sh
   cp /mnt/d/Application\ Setup/Sample\ Files/Jenkins-KVP.pem /home/ubuntu/
   ```

2. **Generate the corresponding public key:**
   ```sh
   ssh-keygen -y -f ~/your-key.pem > ~/your-key.pub
   ```
   For example:  
   ```sh
   ssh-keygen -y -f ~/Jenkins-KVP.pem > ~/Jenkins-KVP.pub
   ```

3. **Add the public key to the managed node's `authorized_keys`:**
   ```sh
   cat ~/your-key.pub | ssh -i ~/your-key.pem <remote-username>@<remote-host> \
     'mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'
   ```
   Replace `<remote-username>` and `<remote-host>` with the managed node's username and IP/hostname.

   For example:  
   ```sh
   cat ~/Jenkins-KVP.pub | ssh -i ~/Jenkins-KVP.pem ubuntu@54.83.85.130 'mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'
   ```

> **Tip:**  
> Secure your private key permissions:
> ```sh
> chmod 600 ~/your-key.pem
> ```

---

This setup enables passwordless SSH authentication from your control node to managed nodes, which is required for seamless Ansible operation.
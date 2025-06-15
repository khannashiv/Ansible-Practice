# Error Handling in Ansible

This document covers various techniques and best practices for handling errors in Ansible playbooks. Effective error handling is crucial for building robust, maintainable automation workflows.

---

## 📚 Reference Documentation

- [Ansible Error Handling Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_error_handling.html)
- [Ansible Loops Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_loops.html)
- [Ansible Variables Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html)
- [Ansible Debug Module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/debug_module.html)
- [Ansible Conditionals Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_conditionals.html)
- [Ansible Blocks Guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_blocks.html)
- [Ansible Rescue and Always](https://docs.ansible.com/ansible/latest/user_guide/playbooks_blocks.html#rescue-and-always)

---

## 🚀 Command Used

```sh
ansible-playbook -i inventory.ini error-handling.yaml 
```

---

## 📝 Outcomes of Hands-On Practice

- ![Ansible-error-handling-1](../Images/Ansible-error-handling-1.png)
- ![Ansible-error-handling-2](../Images/Ansible-error-handling-2.png)
- ![Ansible-error-handling-3](../Images/Ansible-error-handling-3.png)
- ![Ansible-error-handling-4](../Images/Ansible-error-handling-4.png)
- ![Ansible-error-handling-5](../Images/Ansible-error-handling-5.png)
- ![Ansible-error-handling-6](../Images/Ansible-error-handling-6.png)

---

## 💡 Additional Suggestions for Error Handling in Ansible

Here are some more techniques and best practices you may consider adding to your error handling toolkit:

### 1. Using `block`, `rescue`, and `always`
- Use `block` to group tasks, `rescue` to handle errors, and `always` to run tasks regardless of previous failures.
- Example:
    ```yaml
    tasks:
      - block:
          - name: Try a risky operation
            command: /bin/false
        rescue:
          - name: Handle the error
            debug:
              msg: "The task failed, but this is handled."
        always:
          - name: Always run this
            debug:
              msg: "Cleanup or final steps."
    ```

### 2. Ignoring Errors with `ignore_errors: yes`
- Skip to the next task on failure, but use carefully to avoid hiding important issues.

### 3. Conditional Execution with `failed_when` and `changed_when`
- Control when a task is marked as failed or changed based on output or custom logic.

### 4. Registering Results and Checking Them
- Use `register` to capture task output and make decisions in subsequent tasks.

### 5. Using `max_fail_percentage`
- Limit the percentage of hosts that can fail before stopping the play.

### 6. Debugging and Logging
- Use the `debug` and `assert` modules to provide verbose output and validate assumptions.

### 7. Notifying on Failures
- Integrate with notification systems (email, Slack, etc.) on errors for proactive alerting.

### 8. Check Mode (`--check`)
- Run playbooks in dry-run mode to identify potential issues before actual execution.

---

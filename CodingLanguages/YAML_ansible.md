# YAML/Ansible

### Beginning Notes/Terms
- Configuration Management: The process of systematically managing, organizing, and controlling changes in the system. Helps in establishing and maintaining consistency of the system's performance and its functional and physical attributes
- Infrastructure as Code (IaC): The process of managing and provisioning IT infrastructure through machine-readable definition files. Code files are used in place of manual processes.
- Indentation in YAML files is very important and usually needs to be 2 spaces

### Important Terms

- Playbooks consist of one or more plays, that contain tasks composed of modules
  - Plays are the sets of actions/tasks that you want to execute on a set of hosts
- ** Playbook**: A list of plays that define the order in which Ansible will perform operations to achieve an overall goal.
- **Play**: An ordered list of tasks that maps to managed nodes in an inventory.
- **Task**: A list of one or more modules that defines the operations that Ansible performs.
- **Module**: A unit of code or binary that Ansible runs on managed nodes.
- **Inventory**: A list of hosts and groups that Ansible can call on. Usually done in YAML

### Basic Syntax

- **---** signals the start of the playbook
- **...** signals the end of the playbook
- An empty line should be added to the end of the playbook
- **name** at the top defines the name of the Ansible playbook
- **hosts** defines which hosts execute the playbook
  - If you choose to place "all" in for the host, that will refer to all hosts and groups that you have specified in your inventory
  - You can also specify certain groups that you want as well instead of "all"
- **tasks** is the list of tasks for the playbook to execute
- All members of a list are lines beginning at the same indentation level starting with a dash and a space("- ")
  - Two spaces are used as one level of indentation
- Dictionaries are represented in key: value form and the colon must be followed by a space

### Example

```yaml
---
- name: My First Playbook
- hosts: all


  tasks:
    - name: Ping my hosts
      ansible.builtin.ping:

    - name: Print message
      ansible.builtin.debug:
        msg: Hello world!

...
```

- The **ansible.builtin.\*** parts of the code are the Ansible modules which are small programs that automate specific tasks

### Running Ansible Playbooks

- To run a play book, do **ansible-playbook yourplaybookname.yml -i inventoryFile.yml**
  - The -i specifies the inventory file to use
  - **--verbose or -v** flag can be used to see detailed output
  - To run it in check mode which executes a playbook without applying any alterations to your system, do **ansible-playbook --check yourplaybookname.yml**
 

### Important packages

Understanding package use and parameters is very important and can be found at [https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html)

- apt: The package manager for debian/ubuntu and is used very frequently

### Ansible Variables

- Can contain letters, numbers, and underscores
- Python and playbook keywords are not allowed
- Cannot begin with a number
- Created like so:
  - **install_path: /opt/myapp**
- Refrencing a variable:
  - **dest: '{{ install_path }}/foo.cfg
- Variables can be lists and dictionaries as well
- Example YAML file:
```yaml
---
- name: Create user on target system
  hosts: target
  vars:
    username: demo_user
    user_shell: /bin/bash

  vars_files:
    - secret.yml

  tasks:
    - name: Ensure user exists
      user:
        name: "{{ username }}"
        password: "{{ user_password }}"
        shell: "{{ user_shell }}"
        state: present
``` 

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
- A **become: yes** keyword can be added in order to give elevated privileges
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
 

### Important packages/modules

Understanding package use and parameters is very important and can be found at [https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html)

- apt: The package manager for debian/ubuntu and is used very frequently
- register: Allows you to take the output of a task and store it in a variable for future use in your playbook
  - **register: agent_dir**

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

### Ansible Roles

An Ansible Role is a reusable and standalone component that encapsulates a set of Ansible tasks and configurations. Think of roles as the equivalent of functions/methods in traditional programming languages.

- To create a new role, you can run the command **ansible-galaxy init my_role**
- This creates a premade scaffolding of files
  - The **defaults/** directory houses a main.yml file that has your default variables with low precedence that can be easily overriden.
  - The **files/** directory houses static files that you want to copy to remote hosts using the copy or fetch modules
  - The **handlers/** directory contains main.yml for handlers whcih contain tasks triggered by notify statements (e.g., restarting a service after a config change)
  - The **meta/** directory contains main.yml for for role metadata, such as dependencies on other roles.
  - The **tasks/** directory contains main.yml for the main list of tasks to execute in the role. You can include other task files from here.
  - The **templates/** directory is where you will place Jinja2 template files. Use the template module to render them on remote hosts.
  - The **tests/** directory contains a sample test.yml playbook and inventory file for testing your role.
  - The **vars/** directory contains main.yml for variables with higher precedence than those in defaults/.
- This can then be used in your playbook like:
```yaml
---
- hosts: all
  roles:
    - my_role
```

- To find pre-built roles, you can find lots on ansible galaxy that you can use for your playbooks
- For example, this command can be run to download a docker role made by the user geerlingguy: **ansible-galaxy install geerlingguy.docker**

### Ansible Templates

An Ansible Template is a file that contains all your configuration parameters, but has dynamic values that get plugged in fom your Ansible playbooks or from your inventory, variables, etc. Templates use the Jinja2 templating language.

- An example of a template may look like:
```j2
<VirtualHost *:80>
  ServerName {{ server_name }}
  DocumentRoot {{ document_root }}
</VirtualHost>
```

- An example of this being used in a playbook:
```j2
- name: Copy Apache configuration file
  template:
    src: apache2.conf.j2
    dest: /etc/apache2/apache2.conf
  notify: Restart Apache
```



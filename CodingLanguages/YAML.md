# YAML/Ansible

### Important Terms

- Playbooks consist of one or more plays, that contain tasks composed of modules
  - Plays are the sets of actions/tasks that you want to execute on a set of hosts
- ** Playbook**: A list of plays that define the order in which Ansible will perform operations to achieve an overall goal.
- **Play**: An ordered list of tasks that maps to managed nodes in an inventory.
- **Task**: A list of one or more modules that defines the operations that Ansible performs.
- **Module**: A unit of code or binary that Ansible runs on managed nodes.

### Basic Syntax

- **---** signals the start of the playbook
- **...** signals the end of the playbook
- An empty line should be added to the end of the playbook
- **name** at the top defines the name of the Ansible playbook
- **hosts** defines which hosts execute the playbook
- **tasks** is the list of tasks for the playbook to execute
- All members of a list are lines beginning at the same indentation level starting with a dash and a space("- ")
  - Two spaces are used as one level of indentation
- Dictionaries are represented in key: value form and the colon must be followed by a space

### Example

`
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
`

### Running Ansible Playbooks

- To run a play book, do **ansible-playbook yourplaybookname.yml**
  -  **--verbose** flag can be used to see detailed output
- To run it in check mode which executes a playbook without applying any alterations to your system, do **ansible-playbook --check yourplaybookname.yml**

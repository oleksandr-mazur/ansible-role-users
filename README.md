Users
=========

Manage linux users

Requirements
------------

Example requirements.yml
------------------------

```yaml
# Install a role from a specific git branch
- name: users
  src: https://github.com/oleksandr-mazur/ansible-role-users
  version: master
```
Install requirements
--------------------

```bash
$ ansible-galaxy install -r requirements.yml
```

Role Variables
--------------

```yaml
users:
- username: devops 
  sudoers: ALL
  shell: /bin/bash
  group: devops
  state: present
  ssh-keys: 
    - ../files/ssh-keys/user1@company.com
    - ../files/ssh-keys/user2@company.com
```

Example Playbook
----------------

```yaml
- name: Manage users
  hosts: testgroup
  gather_facts: no
  roles:
    - role: users
      users:
      - username: devops 
        sudoers: ALL
        state: present
        ssh-keys: 
          - ../files/ssh-keys/user1@company.com
          - ../files/ssh-keys/user2@company.com
      - username: dev
        sudoers:
          - NGINX
          - SUPEVISOR
        ssh-keys:
          - ../files/ssh-keys/user3@company.com
```

if you want delete user, change **state** to **absent** and run ansible.

if you want add or remove ssh key to user, just add or remove path to key in **ssh-keys** section and run ansible.

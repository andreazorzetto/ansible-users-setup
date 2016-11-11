Ansible-Users-Setup
=================

Role Tasks
-----------------
- Create users
- Set users passwords
- Install ssh keys
- Add full sudoers
- Add custom sudo commands
- Add additional groups for users
- Delete users
- Allow custom users list/files

How to use this role:
-----------------

There are 2 way to provision users through this role:

Passing it a file with users (the .yml extensions is required from ansible 2.2):
```
  - role: ansible-users-setup
    ansible_users_file: my-team.yml
```

Specifing the user details directly in the playbook:
```
  - role: ansible-users-setup
    users:
    - name: vagrant
      description: vagrant
      key:
        - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC1DB5VISZ6JokIpyKlCUCONCpaC9697YcJCIJsuMTUQM5IFKeHs
      sudo: yes
      deleted: no
```

Keep reading to learn about all the configurable fields for users.

Users Fields
-----------------

Provision a new user adding the entry into the right `vars` file.

Users fields:

* `name (mandatory)`
* `description`
* `password` #this is a Linux password hash
* `key`
* `sudo (mandatory)`
* `custom_sudo`
* `additional_groups`
* `deleted (mandatory)`

Full user example:
```
users:
  - name: username
    description: Full Name
    password: $6$F2gxqZJi$3q9lsRPYgyPZO4J4wJnz6MP37U1Y5Rh1IEips4vKmnR7d9AK3KMnKdA2KG.4TBTun
    key:
      - ssh-rsa key1adijhsadlijkfnlsadijknf
      - ssh-rsa key2asdhjfbsakdjbfksaddsdas
    sudo: no
    custom_sudo:
    - "ALL=(ALL) NOPASSWD: /usr/bin/dpkg *"
    additional_groups:
      - www-data
      - wheel
    deleted: no
```

To remove an user just change the value of `deleted` to `yes` then run the role and remove the entry from the vars.

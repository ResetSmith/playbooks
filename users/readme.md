# Users Ansible Playbook

This playbook is for creating and updating users on remote servers/VMs.

The playbook does a few things. It will check the system for the given list of users and then create them if they do not already exist. It also sets their password, and imports their respective SSH public key. From there it will set the user's shell to Bash and give them a custom prompt to help with readability. The final task on the playbook updates permissions for the 'Ansible' user if they are not already set in the correct way.

A typical run of this playbook would look like this:
```
ansible-playbook -i dev playbooks/users/users.yml
```

Included in with this playbook is the ex_users_list.yml file. That is the file that this playbook refences to pull the user data. If you open that file you find it split into two sections, one for user accounts and another for system accounts. If you need to modify the users, follow this format:
```
{name: '$USERNAME', password: '$HASHED_PASSWORD', groups: {'$GROUP1', '$GROUP2'}, system: no, shell: '/bin/bash'}
```

The SSH public key files are located in the 'files' folder of this repository. A user's public key file must be in the format, $USERNAME.id_rsa.pub, the username must match the username in the casat_users.yml file on the bastion server.

If you wish to edit the custom prompt enabled by this playbook, it can be updated by modifying the bashrc.j2 file.

OpenStack Ansible backup
=========

Role to backup operation for OpenStack-Ansible installation. This role will run on deploy node. It will backup data on container then synchronize backup files to deploy node.

Requirements
------------

- OpenStack that has been deployed by OpenStack-Ansible

Role Variables
--------------

```yaml
osa_backup_galera_dir: /opt/openstack-backup/galera
osa_backup_remote_galera_dir: "{{ osa_backup_galera_dir }}"
osa_backup_galera_retention_day: 7
```

Dependencies
------------

NA

Example Playbook
----------------

```yaml
- name: Backup openstack
  hosts: localhost
  user: root
  roles:
    - role: openstack-ansible-backup
```

How to use
----------------

Run these commands on deploy node

```bash
# Install this role
ansible-galaxy install -f winggundamth.openstack-ansible-backup
# Create playbook file
wget -O /opt/openstack-ansible/playbooks/openstack-backup.yml https://raw.githubusercontent.com/winggundamth/openstack-ansible-backup/master/playbooks/openstack-backup.yml
# Run playbooks to backup
cd /opt/openstack-ansible/playbooks/
openstack-ansible openstack-backup.yml
```

Then you can see your backup files at ```/opt/openstack-backup/``` by default. You can change this by putting configure variables in this role to ```/etc/openstack_deploy/user_variables.yml``` file.

License
-------

Apache2

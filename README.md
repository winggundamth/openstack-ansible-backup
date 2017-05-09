Not maintain anymore. Please use https://github.com/opsta/openstack-ansible-backup instead
=========


OpenStack Ansible backup
=========

Role to backup operation for OpenStack-Ansible installation. This role will run on deploy node. It will backup data on container then synchronize backup files to deploy node. Then it will put this task to cron job.

Requirements
------------

- OpenStack that has been deployed by OpenStack-Ansible

Role Variables
--------------

```yaml
osa_backup_galera_dir: /opt/openstack-backup/galera
osa_backup_remote_galera_dir: "{{ osa_backup_galera_dir }}"
osa_backup_galera_retention_day: 7
osa_backup_cron_minute: "0"
osa_backup_cron_hour: "2"
osa_backup_cron_day: "*"
osa_backup_cron_month: "*"
osa_backup_cron_weekday: "*"
osa_backup_cron_command: "/usr/local/bin/openstack-ansible -i /opt/openstack-ansible/playbooks/inventory/dynamic_inventory.py /opt/openstack-ansible/playbooks/openstack-backup.yml"
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
    - role: winggundamth.openstack-ansible-backup
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

Then you will have cron to do daily backup at 2am by default. Also it will do backup job and store files at ```/opt/openstack-backup/``` by default. You can change this by putting configure variables in this role to ```/etc/openstack_deploy/user_variables.yml``` file.

License
-------

Apache2

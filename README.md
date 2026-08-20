# ansible-fortigate-objects
Manage address objects across many Fortigate firewalls via Ansible and SSH.

FortiOS address groups are configured under config firewall addrgrp; the playbooks use FortiOS CLI member operations rather than issuing set member, which would risk replacing the group’s complete inventory.  Validation is performed after making the changes.

Prompts for ssh password when ran, firewall IP addresses listed in inventory.yml


Install it:

apt install ansible sshpass


Run it:

###  Create address objects and add to a group - uses var/var_add_objects.yml
ansible-playbook -i inventory.yml create_addresses.yml

###  Remove addresses from a group - uses var/var_remove_objects.yml
ansible-playbook -i inventory.yml remove_addresses.yml

###  Create or Remove an address group - prompts for input
ansible-playbook -i inventory.yml add_remove_group.yml

###  Delete address objects entirely (if able to be deleted, ie no references) - uses var/var_delete_objects.yml
ansible-playbook -i inventory.yml delete_addresses.yml


Test against one firewall:

ansible-playbook \
  -i inventory.yml \
  delete_addresses.yml \
  --limit fortigate01
  

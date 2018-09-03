KVM Ansible Scripts
====================
Ansible files here are most commonly run locally on the host, not remotely.  Any Ansible playbooks that end in -kickstart
are only to be run during the kickstart install

Root Password Update
====================
To Update the Root Password - you can run the change-root-password.yml (which is a remote task to be run on a workstation):

`ANSIBLE_HOST_KEY_CHECKING=false ansible-playbook -i remote_inventory.ini change-root-password.yml  --ask-pass`


Kickstart Notes:

At the bottom of the kickstart file (in the %post section) you will see this:
`/usr/bin/ansible-pull -C dev -d /root/ansible -U https://git.tmaws.io/techops-infra-ansible/cloudstack.git ansible/deploy-cloudstack-hypervisor.yml -i ansible/inventory.ini > /root/ansible.run 2>&1`

Ongoing KVM Hypervisisor Updates through ansible
====================
This can be achieved by using a mass ssh utility (such as pssh) and running the following:
`pssh -i -h hostlist -A 'ansible-playbook -i inventory.ini deploy-cloudstack-hypervisor.yml'`
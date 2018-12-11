# Demo of Ansible for users and groups

Ansible is a tool that automates system administration, such as creating users, installing applications, monitoring connections, etc. This demo shows how to create users and groups, using our preferred approach.


## Specifics

The Ansible task does this for each user:

* Track each user with a secure unique id, called a zid.

* Create the user's system user account and corresponding group account.

* Set the user's comment to show the zid, name, email address, and telephone number.

* Create the user's ~/.ssh directory and add the user's SSH authorized key


## Preflight

Verify Ansible playbook version is >= 2.5 and is using python >= 3.0

    ansible-playbook --version 

Verify Ansible can connect to all our hosts and run an ad hoc command:

    ansible all -i hosts.yml -a uptime


### Troubleshooting

If Ansible is not using python3, then install it, possibly as root:

    sudo su -
    source /etc/environment
    pip3 install ansible

If yamllint is not available, then install it:

    pip3 install yamllint


## Starter examples

Example:

    ansible-playbook --check -i hosts.yml playbooks/all.yml

Example with paramiko:

    ansible-playbook --check -i hosts.yml -c paramiko playbooks/all.yml

What the command does:

   * `ansible-playbook` runs a playbook of tasks
   * `--check` does a dry run
   * `-i hosts` loads our inventory hosts file
   * `-c paramiko` connects using the SSH Paramiko code
   * `playbooks/all.yml` loads our top level file and runs it

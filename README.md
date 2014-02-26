This repository contains a [Heat][] template to set up the instances
used for the RDO multinode packstack hangout and a set of [Ansible][]
playbooks to configure them.

To provision the hosts, networks, volumes, etc:

    heat stack-create -f openstack.yml

You will probably need to override a number of parameters with values
appropriate to your environment.

To create the `hosts` file and `ssh_config`:

    sh gen_ansible_hosts

Note that this requires a version of `python-heatclient` that includes
<https://review.openstack.org/#/c/60591/>, which adds the
`output-list` and `output-show` commands.

To configure things as they were for the beginning of the hangout:

    ansible-playbook -i hosts -s playbook-hangout.yml

The remaining playbooks will run `packstack` automatically as part of
the configuration process:

To configure a pair of Gluster storage servers and configure Cinder,
Nova, and Glance with Gluster support:

    ansible-playbook -i hosts -s playbook-gluster.yml

To configure the environment without shared storage but with support
for live migration via block migration:

    ansible-playbook -i hosts -s playbook-block.yml

[heat]: https://wiki.openstack.org/wiki/Heat
[ansible]: http://www.ansible.com/home


# Ansible Facts - Sample Output

[Ansible](https://ansible.readthedocs.io/) playbooks often need to cater for multiple different target systems. This is most easily done by using Ansible [facts](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_vars_facts.html) where possible.

I spend an inordinate amount of time digging for what facts are available, and what the possible value for each are. This project is an attempt to save some of those samples for easy reference.

Please contribute samples for systems you have access to :-)

## Content

Key files include:

- [`output/`](output): The output samples
- [`gather.yml`](gather.yml): A playbook to gather facts with the `ansible.builtin.setup` module
- [`vyos-gather.yml`](vyos-gather.yml): Gather facts in VyOS devices with `vyos.vyos.vyos_facts`
- [`ostest.yml`](ostest.yml): Gather key OS facts, display them, and demonstrate how these can be used for conditional tasks
- [`parse-samples.yml`](parse-samples.yml): Parse output samples for key OS information, and save results to `output/parse-samples-summary.json`
- [`molecule/`](molecule): Scenarios for gathering Linux data from within containers (with Podman) and VMs (with KubeVirt)

## Notes On Specific Targets

### Linux

I work mostly with Linux, so I have more samples for it than for other targets.

Besides different distributions, I'm also interested in additional information like whether my playbook is running in a VM or container or not, so some samples cater for this.

### AIX

For AIX we need to ensure that Python 3 is installed first. In IBM Cloud (as of 2025-01):

- AIX 7.3 (7300-02-02) has Python installed
- AIX 7.2 (7200-05-08) has DNF installed, but not Python: `/opt/freeware/bin/dnf install -y python3.11`
- AIX 7.1 (7100-05-09) has YUM installed, but not Python: `yum install -y python3.11`
	- Requires OpenSSL upgrade to 1.1.x first - <https://www-01.ibm.com/marketing/iwm/platform/mrs/assets?source=aixbp>

### RouterOS

For Mikrotik RouterOS, connect by specifying `ansible_connection` & `ansible_network_os` as per this example:

```sh
ansible-playbook -i 192.168.122.216, -e ansible_user=admin -e ansible_connection=ansible.netcommon.network_cli -e ansible_network_os=community.network.routeros gather.yml
```

### VyOS

For VyOS devices, install the prerequisites, then connect by specifying `ansible_connection` & `ansible_network_os` as per this example:

```bash
python3 -m pip install -r vyos-requirements.txt
ansible-galaxy install -r vyos-requirements.yml
ansible-playbook -i 192.168.122.73, -e ansible_user=vyos -e ansible_connection=ansible.netcommon.network_cli -e ansible_network_os=vyos.vyos.vyos vyos.yml
```

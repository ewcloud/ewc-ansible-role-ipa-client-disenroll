# IPA Client Disenrollment Ansible Role

This repository contains a configuration template 
(i.e. an [Ansible Role](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)) 
to customize your environment in the
[European Weather Cloud (EWC)](https://europeanweather.cloud/).
The template is designed to run on a virtual machine, running an IPA client previously enrolled in your IPA server, such that it:
* Requests configuration changes to said IPA server for:
    * Stopping user authentication/authorization management (LDAP) to target virtual machine
    * Deletion of IPA server-internal DNS records referencing  the target virtual 
    machine, if and when found


## Copyright and License
>💡 No dependencies are distributed as part of this repository.

See the [LICENSE](./LICENSE) file for licensing information as it pertains to
files in this repository.

## Usage

The step-by-step described below assume your local file system follows the 
example structure below, with `ewc-ansible-role-ipa-client-disenroll` being a clone of this
repository:
```
.
├── roles
│   └──  ewc-ansible-role-ipa-client-disenroll
├── inventory.yml
└── playbook.yml
```

### 1. Specify the target host and SSH credentials
Create an inventory file to specify address/credentials that Ansible should use
to reach the virtual machine you wish to target:
```yaml
# inventory.yml
---
ewcloud:
  hosts:
    ipa_client:
      ansible_python_interpreter: /usr/bin/python3
      ansible_host: <add the IPV4 address of the target host>
      ansible_ssh_private_key_file: <add the path to local SSH RSA private key file>
      ansible_user: <add the username which owns the SSH RSA private key >
```
### 2. Customize the template

Edit input values for the template [variables](./vars/main.yml) as needed (see
[Inputs](#inputs) section for details).
Then, proceed to create an Ansible Playbook file to load your customizations: 

```yaml
# playbook.yml
---
- name: Disenroll IPA clients from an IPA server
  hosts: ipa_client
  become: true
  become_user: root
  become_method: ansible.builtin.sudo

  roles:
    - ewc-ansible-role-ipa-client-disenroll

```

### 3. Apply the template


You can apply changes on the target host by running:
```bash
ansible-playbook -i inventory.yml playbook.yml
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| ipa_domain | The IPA domain name. Example: `<memberstate>-<organization>-<projectname>.ewc` | `string` | n/a | yes |
| ipa_client_hostname | IPA client host name. Example: `<openstack instance name>` | `string` | n/a | yes |
| ipa_server_hostname | IPA server host name. Example: `ldap`| `string` | n/a | yes |
| ipa_admin_username  | IPA Directory Manager/Admin username | `string` | n/a | yes |
| ipa_admin_password | IPA Directory Manager/Admin password | `string` | n/a | yes |


## Final Environment
> 💡 No new dependencies are installed in the final environment. Only configuration
changes on pre-install packages.

Applying this template will trigger a configuration change on the IPA server against
which the IPA client (i.e. your target host), was previously registered.
Upon successful completion, users will no longer be able to use LDAP credentials to
access the target host, nor will its previous FQDN be resolvable by other hosts in
the subnet.

## Changelog
All notable changes (i.e. fixes, features and breaking changes) are documented 
in the [CHANGELOG.md](./CHANGELOG.md).

## Contributing

Thanks for taking the time to join our community and start contributing!
Please make sure to:
* Familiarize yourself with our [Code of Conduct](./CODE_OF_CONDUCT.md) before 
contributing.
* See [CONTRIBUTING.md](./CONTRIBUTING.md) for instructions on how to request 
or submit changes.

## Authors

[European Weather Cloud](http://support.europeanweather.cloud/) 
<[support@europeanweather.cloud](mailto:support@europeanweather.cloud)>

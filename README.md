# IPA Client Disenrollment Ansible Role
> 💡 No dependencies are installed in your target environment. Only configuration
changes are applied to the [ipa-client](https://www.freeipa.org/) package, if and when found
in your target environment.

This repository contains a configuration template 
(i.e. an [Ansible Role](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)) 
to customize your environment in the
[European Weather Cloud (EWC)](https://europeanweather.cloud/).
The template is designed to run on a virtual machine, running an IPA client previously enrolled in your IPA server, such that it:
* Requests configuration changes to said IPA server for:
    * Stopping user authentication/authorization management (LDAP) to target virtual machine
    * Deletion of IPA server-internal DNS records referencing the target virtual 
    machine, if and when found


## Copyright and License

The provided code and instructions are licensed under the [MIT license](./LICENSE). 
They are intended to automate the setup of an environment that includes 
third-party software components.
The usage and distribution terms of the resulting environment are 
subject to the individual licenses of those third-party libraries.

Users are responsible for reviewing and complying with the licenses of
all third-party components included in the environment.

Contact [EUMETSAT](http://www.eumetsat.int) for details on the usage and distribution terms.

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
| ipa_domain | domain name managed by the existing IPA server. Example: `eumetsat.sandbox.ewc` | `string` | n/a | yes |
| ipa_client_hostname | hostname of the target vm where the IPA client was be installed. Example: `ipa-client-1` | `string` | n/a | yes |
| ipa_server_hostname | IPA server hostname. Example: `ipa-server-1`| `string` | n/a | yes |
| ipa_admin_username  | username of the IPA server administrator account. Example: `ipaadmin` | `string` | n/a | yes |
| ipa_admin_password | password of the IPA server administrator account. Example: `my-secret-password` | `string` | n/a | yes |

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

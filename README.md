# Satellite6.x Ansible Installer

Playbook and roles to install and configure Satellite 6.x
## Propose of this role

This role was created to install and configure a Satellite 6 server

## What this role do.

- Register the server to the RHSM customer portal.
- Configure a Satellite subscription.
- Configure the Satellite repositories.
  Note: Satellite 6.2 is installed with Puppet 3, Satellite 6.3 is installed with Puppet 4 and Satellite 6.4,6.5,6.6,6.7 with Puppet 5.
- Enable the satellite services in the firewall.
- Update the machine.
- Install the Satellite packages.
- Install the Satellite with the default parameters.
- Create the manifest to the Satellite on the Customer portal.
- Import the manifest to the Satellite.
- Configure the packages default policy to on_demand
- Enable the Red Hat Enterprise Linux 7 kickstart on the Satellite Server.
- Enable the Red Hat Enterprise Linux 7 products on the Satellite Server.
- Enable the Red Hat Satellite Tools for 7 Server.
- Synchronize all repositories.
- Create Dev, QA and Prod lifecycle environment.
- Create a content view and add the repositories into.
- Publish the content view to the environments Dev, QA and Prod
- Create four activation keys one for each environment Library, Dev, QA and Prod


## How to use this role.

- 1) Create a playbook as the following instance or use the project example:

~~~
cat playbook_install_sat.yml

---
## Playbook to deploy Satellite 6.3.3
- name: MAIN | Deploying satellite server
  hosts: all
  vars:
    rhsm_user: 'ROOT_USER'
    rhsm_password: 'MYSUPERPASS'
    satellite_package_version: "satellite-6.3.3"
    satellite_version: "6.3"
  roles:
    - ansible-satellite6-install
~~~

- 2) Configure the satellite into the ansible hosts "/etc/ansible/hosts"

- 3) Run the ansible-playbook command and wait. 

  `ansible-playbook playbook_install_sat.yml -l <satellite_host>`

        Get a coffee and be happy \o/

## Variables
To see the default values please check the `main.yml` file in the `vars` directory in the role.

### rhsm_user
Username to register the machine in the customer portal.

### rhsm_password
Password to the user connect and register the machine to the customer portal.

### satellite_version
Satellite main version, this variable is used to set the right repository
i.e: `satellite_version=6.3` to configure the repositories to Satellite 6.3

### foreman_admin_password
Satellite default admin password.

### foreman_initial_organization
Satellite default organization

### foreman_initial_location
Satellite default location

### cv_name
The content view name that will be created during the configuration process.


# Notes:


### Satellite 6 release version
https://access.redhat.com/articles/1365633


## Examples:

~~~
---
## Playbook to deploy Satellite 6.4 latest and reboot the server
- name: MAIN | Deploying satellite server
  hosts: all
  vars:
    rhsm_user: 'ROOT_USER'
    rhsm_password: 'MYSUPERPASS'
    satellite_version: "6.4"
  roles:
    - ansible-satellite6-install
    - reboot
~~~

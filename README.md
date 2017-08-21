vCD
=========

This role deploy server through vCloud Air using the vCD API.
It is intended to be used through Galaxy

Requirements
------------

This role uses the vca (vmware) Cloud modules: http://docs.ansible.com/ansible/vca_vapp_module.html

Role Variables
--------------

The following variables must be set to connect to VCA (I recommend setting those in global_vars/all:

vcd_url: 'URL of the VCD API'
org_name: 'the name of your VCD organisation'
vcd_username: 'username to connect to VCD'
vcd_pwd: 'password to connect to VCD'

The following variable are required to indicate where to deploy the VM:

vdc_name: 'name of the target vDC'
vcd_catalog: 'name of teh catalog where your OS template is stored'
vcd_os_template: 'name of the OS template to use'

For each server the following must be defined:

vm_net: 'name of the org network where the Vm will be attached'
vm_name: 'name of the VM/vApp'  - this also create a vAPP of the same name
vm_operation: 'opeartion to be performed on the VM/vaPP'  - must one of the allowed valued for the operation parameters of the vca_vapp modules
state: 'configures teh state of the VM/vApp' - must one of the allowed valued for the state parameters of the vca_vapp modules

vm_cpu: 'number of vCPU for the VM'
vm_mem: 'VM RAM in GB'

Other variables that can be overridden:

    check_connection_timeout: 600

Change the 'timeout' param of 'wait_for_connection' module. Default is 600 seconds (same as 'wait_for_connection' module default).

    check_connection_delay: 0

Change the 'delay' param of 'wait_for_connection' module. Default is 0 second (same as 'wait_for_connection' module default).

    check_connection_sleep: 1

Change the 'sleep' param of 'wait_for_connection' module. Default is 1 second (same as 'wait_for_connection' module default).

Dependencies
------------

This roel doesn't depend on any other galaxy roles

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: kaneda-fr.vcd }

License
-------

MIT

Author Information
------------------

Sebastien Lacoste-Seris

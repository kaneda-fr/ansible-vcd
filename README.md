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

    check_connection_timeout: 300

Change the 'timeout' param of 'wait_for' module. Default is 300 seconds (same as 'wait_for' module default).

    check_connection_delay: 0

Change the 'delay' param of 'wait_for' module. Default is 0 second (same as 'wait_for' module default).

    check_connection_sleep: 1

Change the 'sleep' param of 'wait_for' module. Default is 1 second (same as 'wait_for' module default).

Use of SSH jump server
----------------------

To use this role via an SSH jump server, the following variables will need to be overriden:

    ansible_ssh_common_args: '{{ ssh_args }} -o ProxyCommand="ssh -W %h:%p -q -p {{ ssh_jump_port }} {{ ssh_jump_user }}@{{ ssh_jump_ip }}"'
    
General purpose setting to allow SSH proxying to occur on all Ansible SSH commands. 

    ssh_args: ''

Extra arguments used to create an ssh connection, for example can be used to point to a different known_hosts file, using ssh_args: '-o "UserKnownHostsFile {{ ssh_known_hosts }}"'
    
    ssh_known_hosts: "{{ lookup('env','HOME') + '/.ssh/known_hosts' }}"

Used to point ssh to a different known hosts file.

    ssh_jump_ip: 'x.x.x.x'

Used to specify the ssh jump server's ip address.

    ssh_jump_user: 'ansible'

The ssh user for the jump server.

    ssh_jump_port: 22

The ssh port for the jump server.

Dependencies
------------

This role doesn't depend on any other galaxy roles

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

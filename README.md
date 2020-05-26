### FortiOS Check
This project contains playbooks to check new installation of FortiGate firewalls.
### Quickstart
There is no inventory file. Please create your own inventory.
To use a test:
```
ansible-playbook 1.1-connectivity.yml
```
### VDOM awareness
inventory file vars should be specified as following in case of VDOM-enabled devices:
```
fg_with_vdoms host=172.16.0.11 vdom_mode=True vdom=data mgmt_vdom=root
fg_without_vdoms host=172.16.0.12 vdom_mode=False
```
### NAPALM notice
Playbook 1.2-bgp uses NAPALM library. Library fails to execute with error message as below in case there are no BGP prefixes received by FortiGate.
```
"msg": "[bgp_neighbors] cannot retrieve device data: list index out of range"
```
You can tweak the library `napalm_fortios/fortios.py` (~ line 371) to get rid of this error.
```
try:
  received = self._execute_command_with_vdom(
		   command_received.format(neighbor))[0].split()
except:
  received = []
```

Running your first iDRAC Playbook
Before you run a playbook to manage your iDRACs, you need to have a valid inventory of target PowerEdge servers. For more information on inventory, see Ansible documentation.

Install OpenManage Ansible Modules either from GitHub or from Ansible Galaxy. For more details, see Dell EMC OpenManage Ansible Modules Installation Guide.
Create an inventory file containing a list of the iDRACs. In the following inventory example, we are using the inventory variables to store the iDRAC IP addresses and the user credentials. For more information on variables, see Ansible documentation.
inventory:[PowerEdge]R740.example.com, idrac_ip='192.168.10.10', idrac_user='root', idrac_password='idrac_password'
Define a playbook to fetch the hardware inventory of the servers. Create the playbook in the same directory where you created the inventory. Following is a playbook example:
playbook.yml

---
- hosts: PowerEdge
  connection: local
  gather_facts: False

  tasks:
  - name: Get hardware inventory
    dellemc_get_system_inventory:
      idrac_ip:  "{{ idrac_ip }}"
      idrac_user:  "{{ idrac_user }}"
      idrac_password:  "{{ idrac_password }}"
      {{ca_path: "//path/to/ca_file.pem"}}
Now run the playbook. Run the following command from the directory where you created the inventory and the playbook:
ansible-playbook playbook.yml -i inventory
Press Enter.
With OpenManage Ansible Modules, you can construct a playbook with a set of modules resulting in an automation workflow for configuration, deployments, and updates of PowerEdge servers.

To view the list of all available iDRAC modules:

Run the following command on the Ansible control machine:
ansible-doc -l | grep "idrac"
Press Enter.
List of the available iDRAC modules is displayed.

To view the documentation of a module:

Run the following command on the Ansible control machine:
ansible-doc <module name>
Press Enter.
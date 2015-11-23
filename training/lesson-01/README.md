Ansible Inventory File:
--------------------------
Ansible can work with multiple systems that you have in your infrastructure by using an INI format file, which is called Inventory file in ansible. During installation, it creates an example that you can use for your reference which is located at `/etc/ansible/hosts`.

We can create our own inventory file from scratch like we did this(add the inventory link). The format of the file is really simple; things in brackets are called group names.
```ini
[web]
web.example.com

[database]
db.example.com
```
If `web.example.com` and `db.example.com` are resolvable through DNS, then we are good otherwise we need to add the ip address explicitly for each host.
```ini
[web]
web.example.com ansible_ssh_host=192.168.33.100

[database]
db.example.com ansible_ssh_host=192.168.33.200
```
For detail explainiation please check the official [link](http://docs.ansible.com/ansible/intro_inventory.html).

Thanks
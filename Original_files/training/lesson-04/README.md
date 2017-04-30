#Ansible Variables
We use variables in ansible to deal with the situation where things differ between systems. Variables are really simply in ansible and
declare as key value pair, for example, `name: tendo`, where `name` is a key and `tendo` is it's value.

Let's take our previous playbook that we have used to install Nginx, this time, we'll modify it to install the exact version of Nginx instead of default version that Ubuntu will automatically install.
It's really easy to use the variable inside ansible task, just enclose the variable name inside `"{{ double curly braces }}"`
```yaml
---
- hosts: web
  become: yes
  vars:
    - nginx_version: nginx=1.4.6-1ubuntu3.3
  tasks:
    - name: Install the Nginx HTTP Server
      apt: 
        name: "{{ nginx_version }}"
        update_cache: yes 
        state: installed
```
 We can also use the value of the variable as variable, for example, after successfully installation of Nginx, we want to print the success message with the provided Nginx version.
```yaml
---
- hosts: web
  become: yes
  vars:
    - nginx_version: nginx=1.4.6-1ubuntu3.3
    - success_message: "Nginx version {{ nginx_version }} installed successfully"
  tasks:
    - name: Install the Nginx HTTP Server
      apt: 
        name: "{{ nginx_version }}"
        update_cache: yes 
        state: installed

    - debug:
        msg: "{{ success_message }}"
```
Now run this playbook:
```shell
vagrant@Control:~/ansible$ ansible-playbook training/lesson-04/lesson-04.yml

PLAY [web] ********************************************************************

GATHERING FACTS ***************************************************************
ok: [web.example.com]

TASK: [Install the Nginx HTTP Server] *****************************************
changed: [web.example.com]

TASK: [debug ] ****************************************************************
ok: [web.example.com] => {
    "msg": "Nginx version nginx=1.4.6-1ubuntu3.3 installed successfully"
}

PLAY RECAP ********************************************************************
web.example.com            : ok=3    changed=1    unreachable=0    failed=0

vagrant@Control:~/ansible$
```
Let's verify that the provided version of Nginx is installed on the target server(web.example.com):
```shell
vagrant@web:~$ nginx -V
nginx version: nginx/1.4.6 (Ubuntu)
built by gcc 4.8.4 (Ubuntu 4.8.4-2ubuntu1~14.04)
TLS SNI support enabled
vagrant@web:~$
```
###Variable Types in Ansible:

There are 4 sources of variables in Ansible:

1 - Variables gathered from `facts` module. You can get them by running command: 
```shell
ansible -m setup hostname
```
2 - Built-in (pre-defined) Ansible variables (AKA 'magic' variables). They are documented in [Ansible documentation](http://docs.ansible.com/playbooks_variables.html#magic-variables-and-how-to-access-information-about-other-hosts): 

Here is the list extracted from Ansible 1.9 documentation:

 - group_names 
 - groups 
 - inventory_hostname 
 - ansible_hostname
 - inventory_hostname_short 
 - play_hosts 
 - delegate_to 
 - inventory_dir
 - inventory_file

3 - Variables passed to ansible via command line called extra-variables. 
4 - Set the variables to the Playbook/Inventory/roles/using included files,but obviously you know what they are.

If you want to read more about variables, please follow this [link](http://docs.ansible.com/ansible/playbooks_variables.html)
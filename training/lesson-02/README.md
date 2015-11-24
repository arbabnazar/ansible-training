# Ansible Ad-hoc Commands
Login to the **control** (machine on which the ansible is installed), by using the following command:
```
vagrant ssh
```
Check that the ansible is properly installed on it:
```
ansible --version
```
```shell
vagrant@Control:~/ansible$ ansible --version
ansible 1.9.4
  configured module search path = None
vagrant@Control:~/ansible$
```
Now come to the Ansible Ad-hoc commands, In simple words, ad-hoc commands are those commands which you want to execute directly without writing a playbook.

**Example-1#** Now that we have verified that the ansible is installed, let's also verify that everything is working properly and for this we'll use `ping` module, it will run against all the hosts that are in our hosts file.
```
ansible -m ping all
```
`ping` module always returns `pong` on successful contact.
```json
vagrant@Control:~/ansible$ ansible -m ping all
db.example.com | success >> {
    "changed": false,
    "ping": "pong"
}

web.example.com | success >> {
    "changed": false,
    "ping": "pong"
}

vagrant@Control:~/ansible$
```
**Example-2#** Change the remote **hostname** using the `command` module:
```
ansible -m command -a "hostname" all
```
And response we get from server will be:
```json
vagrant@Control:~/ansible$ ansible -m command -a "hostname" all
web.example.com | success | rc=0 >>
web

db.example.com | success | rc=0 >>
database

vagrant@Control:~/ansible$
```
**Example-3#** Make a directory on remote servers:
```
ansible web -m file -a "dest=/tmp/test state=directory"
```
The output of the above command will be like this:
```json
vagrant@Control:~/ansible$ ansible web -m file -a "dest=/tmp/test state=directory"
web.example.com | success >> {
    "changed": true,
    "gid": 1000,
    "group": "vagrant",
    "mode": "0775",
    "owner": "vagrant",
    "path": "/tmp/test",
    "size": 4096,
    "state": "directory",
    "uid": 1000
}

vagrant@Control:~/ansible$
```
If you need more explanation about the ad-hoc command, please refer this [link](http://docs.ansible.com/ansible/intro_adhoc.html).
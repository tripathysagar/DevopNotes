agentless : no other software needed on target system
## Inventory
- list of server in a file with `.ini`
- file entries are like
```
# Sample Inventory File

# Web Servers
web1 ansible_host=server1.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web2 ansible_host=server2.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!
web3 ansible_host=server3.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Password123!

# Database Servers
db1 ansible_host=server4.company.com ansible_connection=winrm ansible_user=administrator ansible_password=Password123!


[web_servers]
web1
web2
web3

[db_servers]
db

#combining groups
[all_Server:children]
db_servers
web_servers
 ```
- inventory parameter 
    *  `ansible_connection-(ssh/winrm<windows connection>/localhost)`
    *  `ansible_port-(22/other)`
    *  `ansible_user-(root/administrator)`
    *  `ansible_ssh_pass-<ansible_ssh_pass/ansible_password>`
- security (ansible vault)for saving passward
- good to use ssh key based connections

---

## Playbooks

- ansible's orchestration guide
- runnig commands or services in a remote machine
- uses `.yaml`
- comprise of set of **plays** i.e. "Setup apache" and "Setup tomcat"
- a set of **tasks** i.e."install httpd" and "Start service" make up a **play** "Setup apache"
- file entries are like
```
- name: Setup apache
  hosts: webserver
  tasks:
    - name: install httpd
      yum:
        name: httpd
        state: installed
    - name: Start service
      service:
        name: httpd
        state: started

- name: Setup tomcat
  hosts: appserver
  tasks:
    - name: install httpd
      yum:
        name: tomcat
        state: installed
    - name: Start service
      service:
        name: tomcat
        state: started
```
- different operations ran by  tasks are called **modules**
- run by `ansible-playbook playbook.yaml` or `ansible-playbook -i inventory playbook.yaml`

---

## Modules
- each task is made up of a name and **module** 
- to maintain idempotency
- it can be `service` for updating system softwate
- `lineinfile`  adding & updateing file if entry does not exist
- many oter module exists [docs](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)


---
## variable
- stores info about each host
- use jinja2 template
- can be declared in playbook and inventory
- **condition** using `when` command
```
---
-- name: 'Add name server entry if not already entered'
   hosts: localhost
   become: yes
   tasks:
     - shell: 'cat /etc/resolv.conf'
       register: 'command_output'
     - shell: 'echo "nameserver 10.0.250.10" >> /etc/resolv.conf'
       when: 'command_output.stdout.find("10.0.250.10") == -1'
- name: Install package
  hosts: app1
  tasks:
    - name: Install
      package:
        name: vim
        state: present
      when: ansible_os_family != "RedHat" and ansible_host=="node02"# builIn variable

```
- **loop** using keyword `loop or with_items` and iterator `item`
---
## roles
- installing pre-requsite 
- using playbook modular to be used later with other playbook
- create a directory structure using `ansible-galaxy init mongodb`
- can be imported by adding a `roles directory` as the `playbook.yaml` and importing/declaring in the playbook
- or can be imported from:
```
/etc/ansible/ansible.cfg :
reole_path = /etc/ansible/roles
```

---
## facts
- collecting system info. Can be fetched by `ansible -i inventory -m setup <host>`
- can be found using variable `ansible_facts`
- we can print any varibale using
  ```
  tasks:
  - debug:
      var: ansible_facts
  ```

- `gather_facts: no` is used for not gather facts
- `\etc\ansible\ancible.cfg` file also contains `gathering = implicit`
- whatever declared under playbook will be use for gather facts
- `ansible -m setup localhost`

---
# Some  adhoc examples
- for checking connectivity to multiple servers
  ```
  ---
  - name: Ping Servers
    hosts: all
    tasks: 
    - ping:
  ```
  - `ansible -m ping all`
  - `ansible -m setup localhost` to gather facts
- `become: yes` for sudo access in playbook 
- `ansible_become=yes` in inventory
- `--become-method=doas --become-user=tom --ask-become-pass` : use super user tom and  doas as privilege escalation tool and ask for passwd
- for making inside config
  ```
    [privilege_escalation]
    become=True
  ```
- ```
    - hosts: web1
      tasks:
      - yum: name=sudo state=latest enabled: true
      - yum: name=vsftpd-2.2.2 state=present allow_downgrade=yes
  ```

## Jenkin CLI
`java -jar jenkins-cli.jar -s http://localhost:8085 -auth 'admin:Adm!n321' help`

  UserName: admin

Password: Adm!n321
---


Create a playbook called file.yml under /home/bob/playbooks/ directory and use this playbook to create a file called /opt/file.txt on node01 host. The contents of the file must be This file is created by Ansible!



---
Create a playbook called copy.yml under /home/bob/playbooks/ directory to copy /usr/src/blog/index.html file to both nodes i.e node01 and node02 at location /opt/blog.














---


Write a playbook called replace.yml under /home/bob/playbooks/ directory on student-node host, an inventory file called inventory is already present under /home/bob/playbooks directory. Perform below given tasks using this playbook:


1. We have a file called /opt/music/blog.txt on node01. Using Ansible replace module replace string Kodekloud with Ansible in that file.


2. We have a file called /opt/music/story.txt on node02. Using Ansible replace module replace the string Ansible with Kodekloud in that file.





---
The playbook /home/bob/playbooks/banana.yml has a variable defined called fruit. There are two tasks written in this playbook to print a text.


Use the when conditional to print I am a Banana if the value of fruit is banana otherwise it should print I am not a Banana.








---

The playbook /home/bob/playbooks/fruits.yml currently runs an echo command to print a fruit name. Add a loop directive (i.e with_items) in the task to print all fruits defined under the fruits variable.













---
Create a playbook called package.yml under /home/bob/playbooks/ directory to install vim-enhanced package on student-node.

CheckCompleteIncomplete









---
There is a playbook /home/bob/playbooks/copy_file.yml on student-node. It is supposed to perform below tasks but needs some modification, modify this playbook to add some conditions so that below tasks can be performed:


1. Copy blog.txt file present under /usr/src/condition directory on student-node to node01 under /opt/condition directory. Its user and group owner must be bob and its permissions must be 0640.


2. Copy story.txt file present under /usr/src/condition directory on student-node to node02 under /opt/condition directory. Its user and group owner must be sam and its permissions must be 0400.















---
We already have an inventory file called inventory under /home/bob/playbooks directory on student-node. Write a playbook called lineinfile.yml under /home/bob/playbooks directory. Perform below given tasks using this playbook :


On node01, a file called /var/www/html/index.html is available. It already has some content. Using Ansible lineinfile module add the below given content in it:

Welcome to KodeKloud Labs!


Also make sure to preserve the existing content and this new line must be added at the top of the file.






---


21

skip_next
a. On student-node create an Ansible playbook called service.yml under /home/bob/playbooks/ directory. Further configure it to install vsftpd package on both nodes i.e node01 and node02.


b. The playbook must start the vsftpd service on both nodes.


c. The inventory /home/bob/playbooks/inventory is already there on student-node.




---
Create a playbook called archive.yml under /home/bob/playbooks directory on student-node, an inventory file called inventory is already placed under /home/bob/playbooks directory`. Perform below task using this playbook:


Create an archive of /usr/src/ecommerce/ directory present on each node ie. node01 and node02. The archive name must be demo.tar.gz (make sure that archive format is tar.gz) and save it under /opt/ecommerce/ directory on each node itself.









---
Using Ansible galaxy, install an Ansible role called geerlingguy.nodejs under /home/bob/playbooks/roles directory.





---
Create an Ansible role called package under /home/bob/playbooks/roles directory on student-node. It should install a package called nginx and should start its service as well.


Further consume this role in /home/bob/playbooks/role.yml playbook so that this role can be applied on node01

Swarm
==================

How to setup a docker swarm on digital ocean, including gitlab.
    https://blog.jakehamilton.dev/the-belly-of-the-whale/


Step 1 connect to servers with docker-machine. Doesn't work because access to DO servers over ssh is limited and only a number of connections are allowed in quick succession. 
Solution is to run: `sudo ufw insert 1 allow proto tcp from <your-ip>/32 to any port 22`

Instead of running this for each server we can use the CM tool (configuration management) Ansible to do it on all servers. Also used to open all the docker ports and create admin user.



### Ansible

- What is CM https://www.digitalocean.com/community/tutorials/an-introduction-to-configuration-management.  
- Introduction to Ansible https://www.digitalocean.com/community/tutorials/configuration-management-101-writing-ansible-playbooks.
- Quick tutorial for Ansible https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-18-04
- Shows how to structure Ansible in a project https://serversforhackers.com/c/ansible-roles
- How to create a user with Ansible with vault https://serversforhackers.com/c/create-user-in-ansible

Added `export ANSIBLE_VAULT_PASSWORD_FILE=~/.vault_pass.txt` to `.profile` so don't have to enter password for vault every time. The file only contains the password.


### To-Do
- Create servers with Ansible. Now i need to create them manually first.

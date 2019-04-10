
IaC tutorial
==================

Different tools for IaC, https://github.com/Artemmkin/infrastructure-as-code-tutorial/blob/master/, using google cloud to host servers.

- Get instance ip of Google server: INSTANCE_IP=$(gcloud --format="value(networkInterfaces[0].accessConfigs[0].natIP)" compute instances describe raddit-instance-3)
- Packer, https://github.com/Artemmkin/infrastructure-as-code-tutorial/blob/master/docs/04-packer.md, used to create images which can be used start VMs with.
- Terraform, https://github.com/Artemmkin/infrastructure-as-code-tutorial/blob/master/docs/05-terraform.md, uses image build by packer.
    - Is IaC while Ansible is CM. 
    - Check state of machine. Seems more advanced and complex than Ansible.
    - Is probably more powerful and better to know than Ansible but takes more work to use.
- Ansible, https://github.com/Artemmkin/infrastructure-as-code-tutorial/blob/master/docs/06-ansible.md, used to configure the VM after we start it with Terraform.
- Use Packer to create image, terraform create VM using image, Ansible to config image and VM.
- Propblem: keeping ip adresses up to date. Using Pakcer, Terraform and ansible to create VM and then i get a new ip which needs to be updated in Ansible hosts for Deploy script to work.

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
- Multiple SSH keys https://stackoverflow.com/questions/26256227/ansible-with-multiple-ssh-key-pair/26260799 http://minimum-viable-automation.com/ansible/managing-users-accounts-ansible/
- Example of using ansible for CI/CD flow http://codespair.com/ansible-setup-digital-ocean
- Example playbook for creating DO droplet https://gist.github.com/rdhyee/7047660
- Get masters ip https://stackoverflow.com/a/33957286



#### Environments variables

Added `export ANSIBLE_VAULT_PASSWORD_FILE=~/.vault_pass.txt` to `.profile` so don't have to enter password for vault every time. The file only contains the password.  
Added `export ANSIBLE_HOST_KEY_CHECKING=False` to stop Ansible from checking if known_hosts has changed. If the servers get new ip i can't use same name for the servers in Ansible.



### To-Do
- Create servers with Ansible. Now i need to create them manually first.

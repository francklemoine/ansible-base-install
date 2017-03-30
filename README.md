Base Install
============


Ansible (local prereq)
----------------------

	`apt-get install python-pip python-dev build-essential`

	`pip install --upgrade pip`

	`pip install --upgrade virtualenv`

	`pip install ansible`

	`apt-get install sshpass`


Install on the remote host: Zsh + Users + PermitRootLogin
---------------------------------------------------------
  - Connection = root

	`ansible-playbook -i hosts -u root -k --tags base-install,zsh-install,users-add,permitrootlogin base_install.yml`


Install extra packages/files
----------------------------
  - Connection = sudo

	`ansible-playbook -i hosts --become --ask-become-pass --tags extra-packages base_install.yml`
	`ansible-playbook -i hosts --become --ask-become-pass --tags extra-files base_install.yml`


Public key to remote server
---------------------------

### 'ssh-keygen' command line

	`ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa`


### 'ssh-keygen' with Ansible

	`ansible-playbook -i hosts -u root -k --tags ssh-keygen authentication_install.yml`

	`ansible-playbook -i hosts --become --ask-become-pass --tags ssh-keygen authentication_install.yml`


### 'ssh-copy-id'

	`ssh-copy-id -i ~/.ssh/id_rsa.pub user@host`

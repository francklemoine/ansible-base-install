# Base Install


## :one: Ansible (local prereq)

```bash
apt-get install python-pip python-dev build-essential
pip install --upgrade pip
pip install --upgrade virtualenv
pip install ansible
apt-get install sshpass
```


## :two: Install on the remote host: Zsh + Users + PermitRootLogin

- Connection = root

```bash
ansible-playbook -i inventory/hosts -u root -k --tags base-install,zsh-install,users-add,permitrootlogin base_install.yml
```


## :three: Install extra packages/files

- Connection = sudo

```bash
ansible-playbook -i inventory/hosts --become --ask-become-pass --tags extra-packages base_install.yml
ansible-playbook -i inventory/hosts --become --ask-become-pass --tags extra-files base_install.yml
```


## :four: Set ip forwarding on in /proc and in the sysctl file and reload if necessary

- Connection = sudo

```bash
ansible-playbook -i inventory/hosts --become --ask-become-pass --tags ip-forwarding base_install.yml
```


## :five: Public key to remote server

### `ssh-keygen` command line

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa
```

### `ssh-keygen` with Ansible

```bash
ansible-playbook -i inventory/hosts -u root -k --tags ssh-keygen authentication_install.yml
ansible-playbook -i inventory/hosts --become --ask-become-pass --tags ssh-keygen authentication_install.yml
```

### `ssh-copy-id`

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
```


## :six: Install Borgbackup

```bash
ansible-playbook -i inventory/hosts --become --ask-become-pass --tags borg_install borgbackup_install.yml
ansible-playbook -i inventory/hosts --become --ask-become-pass --tags borg_cron borgbackup_install.yml
```

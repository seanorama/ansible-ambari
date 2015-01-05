# Ansible

Describe what this thing does and how.

## Requirements

### Client machine requirements:
- RedHat EL or CentOS 6 (please help to extend to other OSes)
- Key-based SSH access with sudo rights
- Valid hostname which resolves in DNS

### Control machine (such as your workstation)

- Ansible: http://docs.ansible.com/intro_installation.html#installing-the-control-machine
- python-keyczar: ```pip install --pre python-keyczar`

On OSX, the easiest way is with Homebrew:
```
xcode-select --install  # install the xcode cli tools if not already installed
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
pip install python-keyczar
brew install ansible
```

## Installation

Extract this repository to your workstation where Ansible was installed:
  - Git: ```git clone```
  - Zip: 

## Configuration

There are 2 files to update:
  - ```hosts```
    - Add hostnames of where you want to deploy. Add as many slaves as you like, but the other sections can have only 1 host.
    - Set these to appropriate for your machines:
        - ```ansible_ssh_user=someusername```
        - ```ansible_ssh_private_key_file=~/.ssh/id_rsa```
  - ```group_vars/all```
    - It’s not required to change anything here, but you may want a different cluster name, password, ...


## Deploy
```./ansible-playbook site.yml```

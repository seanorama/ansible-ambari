ansible-ambari
==============

### Quickly deploy Hadoop with the help of Ansible and Apache Ambari

TODO: More detailed description.

Installation
------------

First, ensure the machines you are deploying to meet the requirements:
- Clean installation of RedHat EL or CentOS 6 (please help to extend to other OSes)
- SSH access with keys & sudo rights
- Valid hostname which resolves in DNS

Next, ensure your control machine (likely your workstation) has the tools it needs:
- Ansible: http://docs.ansible.com/intro_installation.html#installing-the-control-machine
- python-keyczar: ```pip install --pre python-keyczar```
- Tip: OSX users use Homebrew:
```Shell
xcode-select --install  
ruby -e “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)”
pip install --pre python-keyczar
brew install ansible
```

Then get the files:
- clone the repository: ```git clone https://github.com/seanorama/ansible-ambari.git && cd ansible-ambari```
- or [download as a zip](https://github.com/seanorama/ansible-ambari/archive/master.zi://github.com/seanorama/ansible-ambari/archive/master.zip)

Configuration
-------------

Edit the configuration where appropriate. At the very least you must add hosts and SSH details

| File       | Option                         | Description                                                                                        |
| ---------- | ---------------------          | -------------------------------
| hosts      | [ambari], [master1], [master2] | put 1 hostname below each of these sections                                                        |
| hosts      | [slaves]                       | put as many hostnames as you like below this                                                       |
| hosts      | `ansible_ssh_user=`            | set to the user you can access the machine with. They should have ssh access.                      |
| hosts      | `ansible_ssh_private_key_file` | path to the ssh private key to access the machines                                                 |
| group_vars | whatever you like              | the deployment will work without this, but you may want to change passwords, the cluster name, ... |

## Deploying
```./ansible-playbook site.yml```

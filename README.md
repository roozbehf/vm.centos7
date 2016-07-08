# CentOS 7 with Docker

This is a Vagrant+Ansible definition of a CentOS 7 box preloaded with a set of basic tools
(such as tmux, JDK, git, and nodejs) and Docker.

## How To

#### 0. Installation

Base installation:
- Install `vagrant` on your machine.
- Install `VirtualBox` on your machine.

Install the **Vagrant plugin** that takes care of automatically installing the correct  **VirtualBox Guest Additions** upon provisioning the VM.

```
vagrant plugin install vagrant-vbguest
```

This should be all that is needed. If this is for some reason not working please check [Vagrant VirtualBox Plugin](https://github.com/dotless-de/vagrant-vbguest).


#### 1. Create the box
```
vagrant up
```
#### 2. Update configuration
Update the configuration of the box, if needed, by editing the `group_vars/all.yml` file and potentially the `connect` script (if the default username is changed).

##### Modify the Playbook
You may not need all the packages that are installed. Modify the roles being applied by editing the `playbook.yml` file.

##### List of Users
By default a user name `joker` will be created. You can configure the list of users
by modifying the dictionary `s_base_users` in `group_vars/all.yml`.

#### 3. Setup
Setup the box using Ansible through Vagrant:
```
vagrant provision
```

Alternatively, in future setups or upgrades, you can limit the run of Ansible roles by a
set of tags; for example, the following only re-runs the role that installs Nodejs
```
env ANSIBLE_TAGS="nodejs" vagrant provision
```

#### 4. Log in
Login using vagrant:
```
vagrant ssh
```
or
```
./connect <optional_SSH_port>
```

## What Is Installed

### Main Packages
Here is a summary of the main packages installed:
- Git (latest from Yum repo)
- Java (OpenJDK) 1.8.0
- Go 1.6
- Docker (latest release)
- Ansible 2.0.0.1
- NodeJS (latest 5.x release)
  - pm2
  - bower
  - gulp-cli
  - yo

### Utilities
In addition to a set of utility packages, such as:
- zip
- unzip
- gzip
- tar
- bind-utils
- vim
- tree
- tmux
- cronie
- asciidoc
- rpm-build
- python2-devel
- python-setuptools

## Contributors
- [Roozbeh Farahbod](https://github.com/roozbehf)
- [Roger Kilian-Kehr](https://github.com/rkiliankehr)

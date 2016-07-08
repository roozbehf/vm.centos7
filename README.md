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

#### 4. Save the Box or Take a Snapshot (Optional)
If you want to avoid building the box again in the future, you can either save the box
at this point (which will be available system-wide and can be transported), or save
a snapshot (which is limited to the vagrant configuration stored on the local folder).

##### 4.1. Save the Box
Simply package your new VM:
```
vagrant package dacent --output myDacent.box
```
(replace `dacent` with the name of the current box and change `myDacent.box` as needed).

Now you can either transfer this box to another machine,
or simply add the new box to your set of Vagrant boxes:
```
vagrant box add my-dacent myDacent.box
```
(change the names as needed).

##### 4.2. Create a Snapshot
Snapshots are very handy when you want to roll back to an earlier version of your box.
Follow [the instructions here](https://www.vagrantup.com/docs/cli/snapshot.html) to save and restore them.

#### 5. Log in
Login using vagrant:
```
vagrant ssh
```
or
```
./connect <optional_SSH_port>
```

## What Is Installed

### Packages Installed
Here is a summary of the main packages that will be installed:
- Git (latest from Yum repo)
- Docker (latest release)

### Packages Available
The following packages are ready to be installed but are disabled in the `playbook.yml` file:
- Java (OpenJDK) 1.8.0
- Go 1.6
- Ansible 2.0.0.1
- NodeJS (latest 5.x release)
  - pm2
  - bower
  - gulp-cli
  - yo

### Utilities
The following utility packages will also be installed:
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
- dnsmasq

## Contributors
- [Roozbeh Farahbod](https://github.com/roozbehf)
- [Roger Kilian-Kehr](https://github.com/rkiliankehr)

# CentOS 7 with Docker

This is a Vagrant+Ansible definition of a CentOS 7 box preloaded with a set of basic tools
(such as tmux, JDK, git, and nodejs) and Docker.

## How To

#### 1. Create the box
```
vagrant up
```
#### 2. Update configuration
Update the configuration of the box, if needed, by editing the `group_vars/all.yml` filand potentially the `connect` script (if the default username is changed).

#### 3. Setup
Setup the box using Ansible through Vagrant:
```
vagrant provision
```

#### 4. Log in
SSH to the box using the `connect` script:
```
./connect
```

Enjoy!

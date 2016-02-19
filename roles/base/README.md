# base role to take care of
- proxy setup in green zone
- centos65 repo setup in green zone
- epel repo setup in green zone
- hosts file to enter ip address of host

the usage of s-base role can be customized with the following variables:

- s_base_hosts:	default, enters the ip address into the /etc/hosts file
- s_base_cloud_zone: default is "white", defines which zone the host is located. "white" will setup a linode host, "green" will setup an enterprise host
- s_base_devops_repo: default, configures the devops yum repo



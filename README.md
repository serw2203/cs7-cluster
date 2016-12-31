# cs7-cluster
vagrant, centos 7.2, ansible

vagrant plugin install vagrant-vbguest

hypervisor - Virtual Box
NetWork - NAT (CIDR-10.0.2.0/24, DHCP -enable), HostOnly (Ipv4 - 10.0.3.1, Ipv4 mask - 255.255.255.0, enable DHCP, DHCP server - 10.0.3.2, DHCP server mask -255.255.255.0, DHCP low IP - 10.0.3.15, DHCP high IP - 10.0.3.254)

Centos box - "https://atlas.hashicorp.com/bertvv/boxes/centos72/versions/2.0.15/providers/virtualbox.box"
downloaded ...
register box - "vagrant box add cs7 /path/*.box"
download packages into folder packages

epel-release-7-8.noarch.rpm

htop-2.0.2-1.el7.x86_64.rpm
jdk-8u111-linux-x64.rpm
mc-4.8.7-8.el7.x86_64.rpm
net-tools-2.0-0.17.20131004git.el7.x86_64.rpm
vim-common-7.4.160-1.el7.x86_64.rpm
vim-enhanced-7.4.160-1.el7.x86_64.rpm
vim-filesystem-7.4.160-1.el7.x86_64.rpm

kafka_2.11-0.10.1.0.tgz

vagrant up

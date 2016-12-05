# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # -- without registered box
    # config.vm.box="base"
    # config.vm.box_url="https://atlas.hashicorp.com/bertvv/boxes/centos72/versions/2.0.15/providers/virtualbox.box"

    config.ssh.insert_key = false
    config.ssh.private_key_path = File.expand_path('~/.vagrant.d/insecure_private_key')

    # -- with registered box such as cs7 (vagrant box add cs7 /path/*.box )
    config.vm.box = "cs7"

    config.vm.provider :virtualbox do |cfg|
	      cfg.gui = false
    end

    nodes = [
	      { :hostname => "cs7-0", :ip => "192.168.11.10", :ram => 768, :cpu => 1 },
	      { :hostname => "cs7-1", :ip => "192.168.11.11", :ram => 768 },
	      { :hostname => "cs7-2", :ip => "192.168.11.12", :ram => 768 }
    ]

    nodes.each do |node|
	  config.vm.define node[:hostname] do |nodeconfig|
	        nodeconfig.vm.hostname = node[:hostname]
	        nodeconfig.vm.network :private_network, ip: node[:ip]

	        #nodeconfig.vm.network :forwarded_port, guest: 80, host: 8080

		nodeconfig.vm.provider :virtualbox do |vb|
	            vb.memory = node[:ram] ? node[:ram] : 256
	            vb.cpus   = node[:cpu] ? node[:cpu] : 1
	        end

	    nodeconfig.vm.provision :shell, privileged: true, inline: <<-SHELL
	        rpm -ivh /vagrant/packages/epel-release-7-8.noarch.rpm
		      yum -y update
		      systemctl restart network.service
	        SHELL
      end
    end

  # last machine
    config.vm.define "cs7-2" do |node|
        node.vm.provision :shell, privileged: false, inline: <<-SHELL
            sudo yum -y install ansible
            ssh-keygen -t rsa -f $HOME/.ssh/id_rsa -q -P ""
            ssh-keyscan 192.168.11.10 >> $HOME/.ssh/known_hosts
            ssh-keyscan 192.168.11.11 >> $HOME/.ssh/known_hosts
            sshpass -f /vagrant/pswd ssh-copy-id vagrant@192.168.11.10
            sshpass -f /vagrant/pswd ssh-copy-id vagrant@192.168.11.11
            ansible-playbook /vagrant/playbook-install.yml -i /vagrant/hosts
 	      SHELL
    end
end

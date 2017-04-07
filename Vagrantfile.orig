Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = false
  config.ssh.insert_key = false
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'" 
  
  # Ansible Control Machine
  config.vm.define "control", primary: true do |control|
	  control.vm.hostname = "Control"
	  control.vm.network "private_network", ip: "192.168.33.50"
	  control.vm.synced_folder ".", "/home/vagrant/ansible", id: "vagrant-root", disabled: false

	  control.vm.provider "virtualbox" do |vb|
		     # Do not load the command line GUI
		     vb.gui = false

		     # Virtual Machine Name
		     vb.name = "Control"

		     # Network settings
		     vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
	             vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]

		     # Use VBoxManage to customize the VM
		     vb.customize ["modifyvm", :id, "--memory", "512"]
	  end
      
      control.vm.provision "shell", path: "provision.sh"
  end

  # Web Server Configuration
  config.vm.define "web", autostart: false do |web|
	  web.vm.hostname = "web"
	  web.vm.network "private_network", ip: "192.168.33.100"
	  web.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true

	  web.vm.provider "virtualbox" do |vb|
		  # Do not load the command line GUI
		  vb.gui = false

		  # Virtual Machine Name
		  vb.name = "web"

		  # Network settings
		  vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
		  vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]

		  # Use VBoxManage to customize the VM
		  vb.customize ["modifyvm", :id, "--memory", "1024"]
	  
	  end
  end

  # Database Server Configuration
  config.vm.define "database", autostart: false do |database|
	  database.vm.hostname = "database"
	  database.vm.network "private_network", ip: "192.168.33.200"
	  database.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true

	  database.vm.provider "virtualbox" do |vb|
		  # Do not load the command line GUI
		  vb.gui = false

		  # Virtual Machine Name
		  vb.name = "database"

		  # Network settings
		  vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
		  vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]

		  # Use VBoxManage to customize the VM
		  vb.customize ["modifyvm", :id, "--memory", "1024"]
	  
	  end
  end
end

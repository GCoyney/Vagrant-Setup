# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
require 'yaml'
machines = YAML.load_file("setup.yml")

Vagrant.configure("2") do |config|
	machines.each do |machine|
	config.vm.define machine['name'] do |machine_vm|
		set_box(machine, machine_vm)
		set_cpus_and_memory(machine, machine_vm)
		update_with_package_manager(machine, machine_vm)
		run_install_scripts(machine, machine_vm)
		
		end
	end
end

def set_cpus_and_memory(machine, machine_vm)
	machine_vm.vm.provider "virtualbox" do |vb|
		vb.cpus = machine['cpus']
		vb.memory = machine['memory']
		
	end
end

def set_box(machine, machine_vm)
	machine_vm.vm.box = machine['box']
end

def update_with_package_manager(machine, machine_vm)
	unless machine['package_manager'].nil?
		machine_vm.vm.provision "shell", inline: "sudo #{machine['package_manager']} update -y"
		if machine['package_manager'] == "yum"
			machine_vm.vm.provision "shell", inline: "sudo #{machine['package_manager']} upgrade -y"
		end
	end
end

def run_install_scripts(machine, machine_vm)
	unless machine['scripts'].nil?
		machine['scripts'].each do |script|
  			machine_vm.vm.provision "shell", privileged: false, path: "vagrant_scripts/#{script}"
		end
	end
end

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
 # machine.each do |machine|
	 # config.vm.define "#machine[jenkins]" do |jenkins| new_vm 
	#	jenkins.vm.box = "centos/7"
	#	jenkins.vm.provider "virtualbox" do |vb|
	#		vb.memory = "2048"
	#		vb.cpus = "2"
	#	end
	#	config.vm.provision "shell", path: "vagrant_scripts/install_server"
	#  end 
	
  #config.vm.define "server" do |server|
	#server.vm.box = "centos/7"
	#server.vm.provider "virtualbox" do |vb|
	#	vb.memory = "2048"
	#	vb.cpus = "2"
	#end
	#config.vm.provision "shell", path: "vagrant_scripts/install_server"
  #end 
	
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
   #config.vm.network "forwarded_port", guest: 9000, host: 8000

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  #   # Display the VirtualBox GUI when booting the machine
   #  vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   #config.vm.provision "shell", inline: <<-SHELL

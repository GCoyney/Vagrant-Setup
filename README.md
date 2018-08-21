# Vagrant-Setup
Vagrant project using a Yaml file to manage virtual machines in VirtualBox.

# New Machines
Guest machines are defined within the [setup.yml] file. 
The name, box, cpus, memory, package_manager, port, packages, scripts 
```sh
- name: jenkins
  box: centos/7
  cpus: 2
  memory: 2048
  package_manager: yum
  port: 8000
  packages:
  - git
  scripts:
  - install_server
```
# Machine Properties
# Required
- name
The name is how you can interact with the guest via Vagrant, for example to only start the virtual machine called default you could run vagrant up default
- box
The name of the box to be provisioned on the guest machine that is either installed locally or downloaded from the Vagrant Cloud
- cpus
Amount of cpus to assign to the guest machine
- memory
Amount of RAM in Megabytes to assign to the guest machine
- private_ip
Private IP address of the guest machine, which will allow connectivity from the host
# Optional
- synced_folders
Folders to syncronise to the guest machine from the host, this could be useful for number of reasons, such as syncing a local maven repository:
```sh
 ---
 - name: default
   box: centos/7
   cpus: 2
   memory: 4096 
   private_ip: 10.0.10.10
   synced_folders:
   - host: ~/.m2
     guest: /home/vagrant/.m2
 ...
```
Note: for synced folders the VirtualBox Guest Additions plugin must be installed for Vagrant:

  ```sh vagrant plugin install vagrant-vbguest ```
 
- package_manager
The supported package managers are yum, apt and apk. When you choose a package manager, all packages will be updated
```sh package_manager: yum ```
- packages
Packages that will be installed using the package_manager that has been selected
 packages:
 - wget
 - unzip
 - vim
 
- scripts
Scripts may be created in the vagrant_scripts folder so that they can be accessed. To run a script, include the name of the file in the scripts list for the guest:
```sh
 scripts:
 - startup
 - configure_firewall.sh
```

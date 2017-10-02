# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
VAGRANT_IP = "10.1.3.24"

Vagrant.require_version ">= 1.8.2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  #config.vm.box = "ubuntu/xenial64"
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: VAGRANT_IP
  #config.ssh.insert_key = false
  config.vm.synced_folder ".", "/home/vagrant/fvang"

  # install Ansible within the VM and run our dev playbook
  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.provisioning_path = "/home/vagrant/fvang/ansible"
    ansible.playbook = "dev.yml"
  end

  # add localhost to Ansible inventory
  config.vm.provision "shell", inline: "printf 'localhost\n' | sudo tee /etc/ansible/hosts > /dev/null"

  config.vm.provider "vmware_fusion" do |vf|
    # vf.gui = true
    vf.vmx['displayname'] = "fvang"
    vf.vmx["memsize"] = "1024"
    vf.vmx["numvcpus"] = "2"
  end

  config.vm.provider "virtualbox" do |vb|
    # vb.gui = true
    vb.name = "fvang"
    vb.memory = "1024"
    vb.cpus = 2
  end
end

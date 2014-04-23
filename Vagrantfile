# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "trusty"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  #config.vm.box = "precise64"
  #config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.11"
  #config.vm.network "public_network", :bridge => 'en0: Wi-Fi (AirPort)'

  # Setup the hostname
  config.vm.hostname = "central-logger-vm"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  #config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.

  config.vm.synced_folder ".", "/home/vagrant/ansible-logstash",
    :nfs => {
      #:mount_options => ['noatime'],
      #:exports_options => ['rw','sync','nohide'],
    }

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider :virtualbox do |vb|
    # Don't boot with headless mode
    # vb.gui = true

    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "4"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end


  # Provision with ansible
  config.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "vagrant_ansible_inventory_default"
      ansible.playbook = "vagrant.yml"
      ansible.verbose = "vvvv"
      ansible.host_key_checking = "false"
  end

end
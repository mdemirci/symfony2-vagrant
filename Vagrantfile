# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "precise64"
    config.vm.box_url = "http://files.vagrantup.com/precise64.box"
    #config.vm.network "private_network", ip: "33.33.33.100"
    #config.vm.synced_folder ".", "/vagrant",
    #	:nfs => (RUBY_PLATFORM =~ /linux/ or RUBY_PLATFORM =~ /darwin/)

    config.vm.provider :virtualbox do |vb|
        # This allows symlinks to be created within the /vagrant root directory, 
        # which is something librarian-puppet needs to be able to do. This might
        # be enabled by default depending on what version of VirtualBox is used.
        vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
        vb.memory = 2048
        # this should fix slow dns lookups in the vm 
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      end

    config.vm.provision :puppet do |puppet|
        puppet.manifests_path = "puppet/manifests"
        puppet.module_path = "puppet/modules"
        puppet.options = ['--verbose']
    end
    
    # Any SSH connections made will enable agent forwarding.
    config.ssh.forward_agent = true
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'hashicorp/precise64'

  config.vm.hostname = 'handrails'

  config.vm.network 'forwarded_port', guest: 3000, host: 3000
  # TODO: Port forwarding for PostgreSQL

  # I'm seeing a bug with build-essential in Chef 10 under Vagrant so here I'm
  # specifying the latest version of Chef to avoid this.
  config.omnibus.chef_version = :latest

  config.vm.provision 'chef_solo' do |chef|
    chef.cookbooks_path = 'cookbooks'

    chef.add_recipe 'apt'
    chef.add_recipe 'build-essential'

    chef.add_recipe 'git'
  end

  config.vm.provision :shell, inline: 'apt-get --yes install vim'
  config.vm.provision :shell, inline: 'apt-get --yes install curl'

  config.vm.provision :shell, inline: 'apt-get --yes install git-flow'

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"
end

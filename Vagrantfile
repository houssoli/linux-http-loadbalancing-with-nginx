# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'.freeze

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define 'lb01' do |lb01|
    lb01.vm.box = 'ubuntu/xenial64'
    lb01.vm.hostname = 'lb01'
    lb01.vm.network :private_network, ip: '10.11.12.50'
    lb01.vm.provider 'virtualbox' do |vb|
      vb.name = 'lb01'
      vb.gui = false
      vb.memory = '1024'
    end
  end

  config.vm.define 'web01' do |web01|
    web01.vm.box = 'ubuntu/xenial64'
    web01.vm.hostname = 'web01'
    web01.vm.network :private_network, ip: '10.11.12.51'
    web01.vm.provider 'virtualbox' do |vb|
      vb.name = 'web01'
      vb.gui = false
      vb.memory = '1024'
    end
  end

  config.vm.define 'web02' do |web02|
    web02.vm.box = 'ubuntu/xenial64'
    web02.vm.hostname = 'web02'
    web02.vm.network :private_network, ip: '10.11.12.52'
    web02.vm.provider 'virtualbox' do |vb|
      vb.name = 'web02'
      vb.gui = false
      vb.memory = '1024'
    end
  end
end

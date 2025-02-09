# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

VAGRANT_BOX         = "generic/ubuntu2004"
VAGRANT_BOX_VERSION = "4.2.6"
# master nodes
MASTER_NODE_COUNT   = 3
MASTER_NODE_CPUS    = 2
MASTER_NODE_MEMORY  = 4096
# worker nodes
WORKER_NODE_COUNT   = 2
WORKER_NODE_CPUS    = 2
WORKER_NODE_MEMORY  = 4096
# lb nodes
LB_NODE_COUNT   = 2
LB_NODE_CPUS    = 1
LB_NODE_MEMORY  = 512

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  (1..MASTER_NODE_COUNT).each do |i|

    config.vm.define "master#{i}" do |node|

      node.vm.box               = VAGRANT_BOX
      node.vm.box_check_update  = false
      node.vm.box_version       = VAGRANT_BOX_VERSION
      node.vm.hostname          = "master#{i}.example.com"

      node.vm.network "private_network", ip: "192.168.56.10#{i}"

      node.vm.provider :virtualbox do |v|
        v.name    = "master#{i}"
        v.memory  = MASTER_NODE_MEMORY
        v.cpus    = MASTER_NODE_CPUS
      end

      node.vm.provider :libvirt do |v|
        v.nested  = true
        v.memory  = MASTER_NODE_MEMORY
        v.cpus    = MASTER_NODE_CPUS
      end

    end

  end

  (1..WORKER_NODE_COUNT).each do |i|

    config.vm.define "worker#{i}" do |node|

      node.vm.box               = VAGRANT_BOX
      node.vm.box_check_update  = false
      node.vm.box_version       = VAGRANT_BOX_VERSION
      node.vm.hostname          = "worker#{i}.example.com"

      node.vm.network "private_network", ip: "192.168.56.11#{i}"

      node.vm.provider :virtualbox do |v|
        v.name    = "worker#{i}"
        v.memory  = WORKER_NODE_MEMORY
        v.cpus    = WORKER_NODE_CPUS
      end

      node.vm.provider :libvirt do |v|
        v.nested  = true
        v.memory  = WORKER_NODE_MEMORY
        v.cpus    = WORKER_NODE_CPUS
      end

    end

  end

  (1..LB_NODE_COUNT).each do |i|

    config.vm.define "lb#{i}" do |node|

      node.vm.box               = VAGRANT_BOX
      node.vm.box_check_update  = false
      node.vm.box_version       = VAGRANT_BOX_VERSION
      node.vm.hostname          = "lb#{i}.example.com"

      node.vm.network "private_network", ip: "192.168.56.12#{i}"

      node.vm.provider :virtualbox do |v|
        v.name    = "lb#{i}"
        v.memory  = LB_NODE_MEMORY
        v.cpus    = LB_NODE_CPUS
      end

      node.vm.provider :libvirt do |v|
        v.nested  = true
        v.memory  = LB_NODE_MEMORY
        v.cpus    = LB_NODE_CPUS
      end

    end

  end

end
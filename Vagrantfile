# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"

  memory_mb = 256

  cluster = {
    'storm-nimbus-node-1' => "192.168.5.150",
    'storm-supervisor-node-1' => "192.168.5.160",
    'storm-supervisor-node-2' => "192.168.5.161",
  }

  cluster.each_with_index do |(short_name, ip), idx|

    config.vm.define short_name do |host|

      host.vm.network :private_network, ip: ip
      host.vm.hostname = short_name
      host.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", memory_mb]
      end

      host.vm.provision :ansible do |ansible|
        if short_name.include? "nimbus"
            ansible.playbook = "nimbus-provision.yml"
            ansible.extra_vars = {
              cluster_node_seq: idx + 1,
              cluster_ip_addresses: cluster.values,
              machine_ip: ip
            }
        else
            ansible.playbook = "supervisor-provision.yml"
            ansible.extra_vars = {
              cluster_node_seq: idx + 1,
              cluster_ip_addresses: cluster.values,
              machine_ip: ip
            }
        end
      end
    end
  end
end

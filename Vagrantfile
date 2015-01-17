# Configure VirtualBox host-only networking
# vboxmanage hostonlyif create
# vboxmanage hostonlyif ipconfig vboxnet0 --ip 10.125.0.1 --netmask 255.255.255.0
# vboxmanage dhcpserver remote --ifname vboxnet0

unless Vagrant.has_plugin?('vagrant-hostmanager')
    raise 'vagrant plugin install vagrant-hostmanager'
end

domain = 'example.com'

nodes = [
  { :hostname => 'node1', :ip => '10.125.0.11', :box => 'chef/centos-6.5'},
  { :hostname => 'node2', :ip => '10.125.0.12', :box => 'chef/centos-6.5'},
  { :hostname => 'node3', :ip => '10.125.0.13', :box => 'chef/centos-6.5'}
]

Vagrant.configure('2') do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      # configure the box, hostname and networking 
      node_config.vm.box = node[:box]
      node_config.vm.hostname = node[:hostname] + '.' + domain
      node_config.vm.network :private_network, ip: node[:ip]

      node_config.hostmanager.aliases = node[:hostname]

      node_config.vm.provision :ansible do |ansible|
        ansible.playbook = 'site.yml'
        ansible.inventory_path = 'vagrant'
      end
    end
  end
end

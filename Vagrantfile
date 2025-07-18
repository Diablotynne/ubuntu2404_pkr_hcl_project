require 'yaml'
vars = YAML.load_file('sites.yaml')

Vagrant.configure("2") do |config|
  config.vm.box      = vars['box']
  config.vm.base_mac = vars['base_mac']

  config.vm.provider "virtualbox" do |vb|
    vb.memory = vars['memory']
    vb.cpus   = vars['cpus']
    vb.gui    = false
    
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.ssh.username   = "vagrant"
  config.ssh.password   = "vagrant"
  config.ssh.insert_key = true
end

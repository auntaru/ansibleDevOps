VAGRANTFILE_API_VERSION = "2"
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
 Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "maria.yml"
    ansible.sudo = true
  end
  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "forwarded_port", guest: 3306, host: 3336
    master.vm.network "private_network", ip: "192.168.10.2"       
  end
  config.vm.define "slave" do |slave|
    slave.vm.hostname = "slave"
    slave.vm.network "forwarded_port", guest: 3306, host: 3337
    slave.vm.network "private_network", ip: "192.168.10.3"               
  end
  config.vm.provider :libvirt do |v|
    v.memory = 1024
    v.cpus = 2
  end
end

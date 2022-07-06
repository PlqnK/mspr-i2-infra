Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  config.vm.define "docker-host" do |subconfig|
    subconfig.vm.box = "fedora/36-cloud-base"
    subconfig.vm.network "private_network", ip: "192.168.121.100"
    subconfig.vm.network "forwarded_port", guest: 80, host: 80
    subconfig.vm.network "forwarded_port", guest: 443, host: 443
    #subconfig.vm.hostname = machine[:name] + ".mbconcept.internal"
    #subconfig.hostsupdater.aliases = [machine[:alias] + ".mbconcept.internal"]
    subconfig.vm.provider "libvirt" do |lv|
      lv.cpus = 2
      lv.memory = 4096
    end
    subconfig.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.cpus = 2
      vb.memory = 4096
    end
    subconfig.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "inventory.yml"
      ansible.playbook = "playbook.yml"
      ansible.limit = "all"
    end
  end
end

Vagrant.configure(2) do |config|

  N = 2
  (1..N).each do |i|
    config.vm.define "app#{i}" do |node|
      node.vm.box = "cent0s7"
      node.vm.synced_folder ".", "/vagrant", disabled: true
      node.vm.hostname = "app#{i}"
      node.vm.network "private_network", ip: "10.0.26.20#{i}"
      node.vm.box_check_update = false
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
      end
    end
  end

  config.vm.define "stat" do |stat|
      stat.vm.network "private_network", ip:"10.0.26.102"
      stat.vm.hostname = "mgmt"
      stat.vm.box = "cent0s7"
      stat.vm.synced_folder ".", "/vagrant", disabled: true
      stat.vm.box_check_update = false
      stat.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
        vb.name = "stat"
      end
  end

  config.vm.define "mgmt" do |mgmt|
      mgmt.vm.network "private_network", ip:"10.0.26.101"
      mgmt.vm.hostname = "mgmt"
      mgmt.vm.box = "cent0s7"
      mgmt.vm.synced_folder ".", "/vagrant", disabled: true
      mgmt.vm.box_check_update = false
      mgmt.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
        vb.name = "mgmt"
      end
      mgmt.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
      mgmt.vm.provision "file", source: "provision", destination: "/home/vagrant/provision"
      mgmt.vm.provision "shell", path: "shell/ansible-setup.sh"
  end

end

NUM_WORKER_NODES=2
IP_NW="10.0.0."
IP_START=10
VM_IMAGE="bento/ubuntu-22.04"

Vagrant.configure("2") do |config|
  # create host name entries in hosts file
  config.vm.provision "shell", env: {"IP_NW" => IP_NW, "IP_START" => IP_START}, inline: <<-SHELL
      apt-get update -y
      echo "$IP_NW$((IP_START)) master-node" >> /etc/hosts
      echo "$IP_NW$((IP_START+1)) worker-node01" >> /etc/hosts
      echo "$IP_NW$((IP_START+2)) worker-node02" >> /etc/hosts
  SHELL

  config.vm.box = "#{VM_IMAGE}"
  config.vm.box_check_update = true
  # create master VM
  config.vm.define "master" do |master|
    master.vm.hostname = "master-node"
    master.vm.network "private_network", ip: IP_NW + "#{IP_START}"
    master.vm.provider "virtualbox" do |vb|
        vb.memory = 4096
        vb.cpus = 2
    end
    master.vm.provision "shell", path: "scripts/setup-server.sh"
    master.vm.provision "shell", path: "scripts/setup-master.sh"
  end
  # create worker VMs
  (1..NUM_WORKER_NODES).each do |i|
    config.vm.define "node0#{i}" do |node|
      node.vm.hostname = "worker-node0#{i}"
      node.vm.network "private_network", ip: IP_NW + "#{IP_START + i}"
      node.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 1
      end
      node.vm.provision "shell", path: "scripts/setup-server.sh"
      node.vm.provision "shell", path: "scripts/setup-node.sh"
    end
  end
end 

Vagrant.configure("2") do |config|
  config.vm.boot_timeout = 600

  # Update and upgrade the system, and add entries to /etc/hosts
  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt upgrade -y
    echo "10.0.100.20 master-control-plane" >> /etc/hosts
    echo "10.0.100.21 worker-node01" >> /etc/hosts
    echo "10.0.100.22 worker-node02" >> /etc/hosts
  SHELL

  # Master Node
  config.vm.define "master" do |master|
    master.vm.box = "ubuntu/trusty64"
    master.vm.box_check_update = false
    master.vm.hostname = "master-control-plane"
    master.vm.network "private_network", ip: "10.0.100.20"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end
    master.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      systemctl start docker
      systemctl enable docker
      apt-get install -y apt-transport-https curl
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
      echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
      apt-get update
      apt-get install -y kubelet kubeadm kubectl
      apt-mark hold kubelet kubeadm kubectl
    SHELL
  end

  # Worker Nodes
  (1..2).each do |i|
    config.vm.define "node0#{i}" do |node|
      node.vm.box = "ubuntu/trusty64"
      node.vm.box_check_update = false
      node.vm.hostname = "worker-node0#{i}"
      node.vm.network "private_network", ip: "10.0.100.2#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 1
      end
      node.vm.provision "shell", inline: <<-SHELL
        apt-get update
        apt-get install -y docker.io
        systemctl start docker
        systemctl enable docker
        apt-get install -y apt-transport-https curl
        curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
        echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
        apt-get update
        apt-get install -y kubelet kubeadm kubectl
        apt-mark hold kubelet kubeadm kubectl
      SHELL
    end
  end
end

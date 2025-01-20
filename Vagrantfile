Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "k8s-master" do |master|
    master.vm.hostname = "k8s-master"
    master.vm.network "private_network", type: "dhcp"  # Host-Only Network
    master.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    master.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      apt-get install -y apt-transport-https curl
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
      cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
      deb http://apt.kubernetes.io/ kubernetes-xenial main
      EOF
      apt-get update
      apt-get install -y kubelet kubeadm kubectl
      apt-mark hold kubelet kubeadm kubectl
    SHELL
  end

  config.vm.define "k8s-worker1" do |worker|
    worker.vm.hostname = "k8s-worker1"
    worker.vm.network "private_network", type: "dhcp"  # Host-Only Network
    worker.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    worker.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      apt-get install -y apt-transport-https curl
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
      cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
      deb http://apt.kubernetes.io/ kubernetes-xenial main
      EOF
      apt-get update
      apt-get install -y kubelet kubeadm kubectl
      apt-mark hold kubelet kubeadm kubectl
    SHELL
  end

  config.vm.define "k8s-worker2" do |worker|
    worker.vm.hostname = "k8s-worker2"
    worker.vm.network "private_network", type: "dhcp"  # Host-Only Network
    worker.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    worker.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      apt-get install -y apt-transport-https curl
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
      cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
      deb http://apt.kubernetes.io/ kubernetes-xenial main
      EOF
      apt-get update
      apt-get install -y kubelet kubeadm kubectl
      apt-mark hold kubelet kubeadm kubectl
    SHELL
  end
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

## ENV['K8SINIT'] = 'true': Full Kubernetes component installation, initializes a Kubernetes cluster, and joins all 3 worker nodes into the Kubernetes Cluster
## ENV['K8SINIT'] = 'false': Full Kubernetes component installation, but will not initialize a cluster or add worker nodes, but will be ready for "kubeadm init . . ."
ENV['K8SINIT'] = 'true'

# Additional nodes will need to be added into the /etc/hosts section of the bootstrap.sh setup file.
NodeCount = 3

Vagrant.configure(2) do |config|
  # config.env.enable
  config.vm.provision "shell", path: "bootstrap.sh"
  # Kubernetes Master Server
  config.vm.define "kmaster" do |kmaster|
    kmaster.vm.box = "centos/7"
    kmaster.vm.hostname = "kmaster.example.com"
    kmaster.vm.network "private_network", ip: "172.42.42.100"
    kmaster.vm.provider "virtualbox" do |v|
      v.name = "kmaster"
      v.memory = 2048
      v.cpus = 2
    end
    if ENV['K8SINIT'] == "true"
      # Uncomment as desired to use the different Network Providers:
      kmaster.vm.provision "shell", path: "bootstrap_kmaster.sh"
      # kmaster.vm.provision "shell", path: "bootstrap_kmaster_calico.sh"
      # kmaster.vm.provision "shell", path: "bootstrap_kmaster_flannel.sh"
    end
  end

  # Kubernetes Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "kworker#{i}" do |workernode|
      workernode.vm.box = "centos/7"
      workernode.vm.hostname = "kworker#{i}.example.com"
      workernode.vm.network "private_network", ip: "172.42.42.10#{i}"
      workernode.vm.provider "virtualbox" do |v|
        v.name = "kworker#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      if ENV['K8SINIT'] == "true"
        workernode.vm.provision "shell", path: "bootstrap_kworker.sh"
      end
    end
  end
end

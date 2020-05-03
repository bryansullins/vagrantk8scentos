# Vagrant Kubernetes Lab

This is my Vagrant Kubernetes Lab using the VirtualBox Provider on MacOS. However, there is no reason it would not run on Windows or Linux. Platforms outside of MacOS, however are untested.

### Prerequisites and Requirements
This Vagrant Kubernetes Lab was built and tested on:

#### Software Requirements:

1. MacOS Catalina Version 10.15.4.
2. VirtualBox Version 6.0.18 r136238 (Qt5.6.3). [VirtualBox](https://www.virtualbox.org/)
3. Vagrant Version 2.2.6. [Vagrant](https://www.vagrantup.com/)

#### Hardware Specs:
1. 1.4GHz quad-core Intel Core i5
2. 16GB of 2133MHz LPDDR3 onboard memory - Uses about 4.5GB RAM
3. 128GB SSD - Requires 4GB Drive Space

Other platforms or versions outside of the above are untested.

## Getting Started

Clone the repo to your local machine:

    git clone https://github.com/bryansullins/vagrantk8scentos.git    

### Vagrantfile options and running `vagrant up`

Assuming you have the above requirements, if you want to build the lab with the default paramaters, from the repo root directory type:

    vagrant up    

To nuke the environemt, type:

    vagrant destroy    

By default, running `vagrant up` will build the Kubernetes Lab with one Master Node and three Worker Nodes. `kubeadm init` is as follows:

    kubeadm init --apiserver-advertise-address=172.42.42.100 --pod-network-cidr=192.168.0.0/16    

However, there is a "Practice Mode" option that will install all components for Kubernetes on all Nodes, but will not run `kubeadm init`. This will allow you to initialize Kubernetes manually for practice, if you so wish. To use "Practice Mode", change the parameter `ENV['K8SINIT']` to false, then build a new Vagrant env by typing `vagrant up`:

    ENV['K8SINIT'] = 'false'



### Other options

You can also alter options for using different Network Providers, such as Calico or Flannel. Comments in the Vagrantfile should give you guidance:

    # Uncomment as desired to use the different Network Providers:
    kmaster.vm.provision "shell", path: "bootstrap_kmaster.sh"
    # kmaster.vm.provision "shell", path: "bootstrap_kmaster_calico.sh"
    # kmaster.vm.provision "shell", path: "bootstrap_kmaster_flannel.sh"

## Built With

* [Vagrant](https://www.vagrantup.com/) - Hashicorp's local Dev Env.
* [VirtualBox](https://www.virtualbox.org/) - Oracle's free local Virtualization tool.

## Contributing

Contact [bryansullins](https://github.com/bryansullins) for contributing to this repo.

## Versioning

See [CHANGELOG](CHANGELOG.md)

## Acknowledgments

* Hat tip to Exxactcorp. This repo was taken from their current K8s Vagrant Lab website and this woud not have been possible without it:
* Exxactcorp [BlogPost](https://blog.exxactcorp.com/building-a-kubernetes-cluster-using-vagrant/)
* Exxactcorp Vagrant Kubernetes Lab [Repo](https://bitbucket.org/exxsyseng/k8s_centos/src/master/) 
# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 05-03-2020
Initial Release:
This repo is taken from Exxactcorp's site [here](https://bitbucket.org/exxsyseng/k8s_centos/src/master/).
### Added 

`ENV['K8SINIT'] = 'true'` Parameter

Options to implement different Network Providers:

    # Uncomment as desired to use the different Network Providers:    
    kmaster.vm.provision "shell", path: "bootstrap_kmaster.sh"    
    # kmaster.vm.provision "shell", path: "bootstrap_kmaster_calico.sh"    
    # kmaster.vm.provision "shell", path: "bootstrap_kmaster_flannel.sh"    

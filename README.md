# Pre-requirement

*Third-party software*
* Oracle VM VirtualBox
* Vagrant by HashiCorp

*SecurityVision installer*
* redist folder (unpack and put in `distr` folder of this project)
* installer-console.v5 (rename downloaded installer and put in `distr` folder of this project)

*Supported Operating Systems*

* Debian 10
* Debian 11
* Ubuntu 20.04
* Ubuntu 22.04

# Deployment

* Uncomment one `VM_BOX` var in `Vagrantfile` to select base OS for cluster
* Start deployment with `vagrant up` command

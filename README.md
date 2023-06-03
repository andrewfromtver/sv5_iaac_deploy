# Pre-requirement

*Third-party software*
* Oracle VM VirtualBox
* Vagrant by HashiCorp

*SecurityVision installer (ubuntu20.04 or ubuntu22.04)*
* redist folder (unpack and put in `distr` folder of this project)
* installer-console.v5 (rename downloaded installer and put in `distr` folder of this project)

# Deployment

* Uncomment one `UBUNTU_BOX` var in `Vagrantfile` to select ubuntu 20.04 or 22.04 box
* Start deployment with `vagrant up` command

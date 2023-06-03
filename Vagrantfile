# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

VM_BOX = 'generic/debian10'       # Debian 10
# VM_BOX = 'generic/debian11'     # Debian 11
# VM_BOX = 'generic/ubuntu2004'   # Ubuntu 20.04
# VM_BOX = 'generic/ubuntu2204'   # Ubuntu 22.04

Vagrant.configure(2) do |config|

  config.vm.define "sv5database" do |sv5database|
    sv5database.vm.box = VM_BOX
    sv5database.vm.hostname = 'sv5database.test.local'
    sv5database.vm.provider "virtualbox" do |v|
      v.name = 'sv5database'
      v.memory = 4096
      v.cpus = 4
    end
    sv5database.vm.network "private_network", ip: "192.168.56.102"
    sv5database.vm.synced_folder "./distr/", "/distr"
    sv5database.vm.provision "shell", inline: <<-SHELL
        chmod +x /distr/installer-console.v5
        /distr/installer-console.v5 --config /distr/config/database.json

        cp /distr/postgres/postgresql.conf /etc/postgresql/13/main/postgresql.conf
        cp /distr/postgres/pg_hba.conf /etc/postgresql/13/main/pg_hba.conf
        systemctl restart postgresql

        psql -U postgres -c "ALTER USER postgres WITH PASSWORD 'sv5password';"
        sed -i "s/trust/scram-sha-256/g" /etc/postgresql/13/main/pg_hba.conf
        systemctl restart postgresql
        
      SHELL
  end

  config.vm.define "sv5services" do |sv5services|
    sv5services.vm.box = VM_BOX
    sv5services.vm.hostname = 'sv5services.test.local'
    sv5services.vm.provider "virtualbox" do |v|
      v.name = 'sv5services'
      v.memory = 8144
      v.cpus = 8
    end
    sv5services.vm.network "private_network", ip: "192.168.56.103"
    sv5services.vm.synced_folder "./distr/", "/distr"
    sv5services.vm.provision "shell", inline: <<-SHELL
        chmod +x /distr/installer-console.v5
        /distr/installer-console.v5 --config /distr/config/services.json

    SHELL
  end

  config.vm.define "sv5webportal" do |sv5webportal|
    sv5webportal.vm.box = VM_BOX
    sv5webportal.vm.hostname = 'sv5webportal.test.local'
    sv5webportal.vm.provider "virtualbox" do |v|
      v.name = 'sv5webportal'
      v.memory = 2048
      v.cpus = 2
    end
    sv5webportal.vm.network "private_network", ip: "192.168.56.101"
    sv5webportal.vm.synced_folder "./distr/", "/distr"
    sv5webportal.vm.provision "shell", inline: <<-SHELL
        chmod +x /distr/installer-console.v5
        /distr/installer-console.v5 --config /distr/config/webportal.json

    SHELL
  end

end

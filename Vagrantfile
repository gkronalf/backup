# -*- mode: ruby -*- 
# vi: set ft=ruby : vsa
# disk = './.vagrant/backup_disk.vdi'
Vagrant.configure(2) do |config| 
   config.vm.box = "centos/7" 
   config.vm.box_version = "2004.01" 
   config.vm.provider "virtualbox" do |v| 
      v.memory = 256 
      v.cpus = 1
   end
   config.vm.define "backup" do |backup| 
      backup.vm.network "private_network", ip: "192.168.11.160" 
      backup.vm.hostname = "backup"
      backup.vm.disk :disk, size: "40GB", name: "disk-01", primary: true
      backup.vm.disk :disk, size: "2GB", name: "disk-backup"
      backup.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/me.pub"
      # backup.vm.provision :file, source: './scripts', destination: '/home/vagrant/scripts'
      backup.vm.provision "shell", inline: <<-SHELL
      cat /home/vagrant/.ssh/me.pub >> /home/vagrant/.ssh/authorized_keys
      SHELL
      # backup.vm.provision "shell", path: "./scripts/script_backup.sh"
   end
   config.vm.synced_folder '.', '/vagrant', disabled: true

   config.vm.define "client" do |client| 
      client.vm.network "private_network", ip: "192.168.11.150"
      client.vm.hostname = "client" 
      client.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/me.pub"
      # client.vm.provision :file, source: './scripts', destination: '/home/vagrant/scripts'
      client.vm.provision "shell", inline: <<-SHELL
      cat /home/vagrant/.ssh/me.pub >> /home/vagrant/.ssh/authorized_keys
      SHELL
   end
   config.vm.synced_folder '.', '/vagrant', disabled: true
end 

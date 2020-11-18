# -*- mode: ruby -*-
# vi: set ft=ruby :
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

secmachines = {
	'kali' => { 'cpu' => '2', 'memory' => '2048', 'ip' => '10', 'box' => 'kalilinux/rolling'},
	'metasploitable' => {'cpu' => '1', 'memory' => '2048', 'ip' => '20', 'box' => 'rapid7/metasploitable3-ub1404'},
	'windows' => {'cpu' => '2', 'memory' => '2048', 'ip' => '30', 'box' => 'rapid7/metasploitable3-win2k8'},
}

Vagrant.configure("2") do |config|

  secmachines.each do |name, machines|
     config.vm.define "#{name}" do |server|

     if "#{name}" == 'metasploitable'
      server.ssh.username = "vagrant"
      server.ssh.password = "vagrant"
      server.vm.synced_folder '.', '/vagrant', disabled: true
     elsif "#{name}" == "windows"
      server.vm.communicator = "winrm"
      server.winrm.retry_limit = 60
      server.winrm.retry_delay = 10
      server.vm.provision :shell, inline: "C:\\startup\\disable_firewall.bat"
      server.vm.provision :shell, inline: "C:\\startup\\install_share_autorun.bat"
      server.vm.provision :shell, inline: "C:\\startup\\setup_linux_share.bat"
      server.vm.provision :shell, inline: "rm C:\\startup\\*"
     end

       server.vm.hostname = "#{name}"
       server.vm.box = "#{machines['box']}"
       server.vm.network "private_network", ip: "10.50.7.#{machines['ip']}", dns: "8.8.8.8" 

       server.vm.provider "virtualbox" do |vb|
         vb.customize ["modifyvm", :id, "--groups", "/PenTest"]
         vb.customize ["modifyvm", :id, "--graphicscontroller", "vboxvga"]
         vb.customize ["modifyvm", :id, "--vram", "65"]
         vb.memory = "#{machines['memory']}"
         vb.cpus = "#{machines['cpu']}"
         vb.name = "#{name}"
         vb.gui = false
       end

    end
  end
end

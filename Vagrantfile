
Vagrant.configure("2") do |config|
 
  config.vm.box = "ubuntu/bionic64"

  config.vm.boot_timeout = 600

  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder ".", "/var/www/html"
  
  config.vm.provider "virtualbox" do |vb|
 
    vb.memory = "1024"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
  apt-get update
  apt-get install -y apache2 php libapache2-mod-php
  systemctl enable apache2
  systemctl start apache2
  SHELL
end

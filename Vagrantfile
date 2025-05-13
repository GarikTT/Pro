# -*- mode: ruby -*-
# vi: set ft=ruby :

#Vagrant.configure("2") do |config|
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false
  
  config.vm.provision "shell", inline: <<-SHELL
		sed -i 's|http://mirror\.centos\.org/|http://mirror.yandex.ru/centos/|g' /etc/yum.repos.d/*.repo
		sed -i 's/^#.*baseurl=http/baseurl=http/g' /etc/yum.repos.d/*.repo
		sed -i 's/^mirrorlist=http/#mirrorlist=http/g' /etc/yum.repos.d/*.repo

		yum clean all
		yum makecache
        
		yum update -y
		yum upgrade -y
		yum update kernel kernel-devel -y
		yum install kernel kernel-devel -y
		yum install epel-release yum-utils wget mailx sendmail cyrus-sasl-plain telnet-server telnet nfs-utils mc -y
		
				if [ -d /vagrant/mc ]; then
					echo -e 'Копируем параметры "Midnight Commander",\nчтобы не заниматься ерундой в дальнейших его настройках.'
					mkdir -p ~/.config/mc
					yum install mc -y
					mkdir -p /home/vagrant/.config/mc
					cp --backup=numbered /vagrant/mc/* /home/vagrant/.config/mc
					cp --backup=numbered /vagrant/mc/* ~/.config/mc
				fi		
  SHELL
end

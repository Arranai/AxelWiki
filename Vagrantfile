Vagrant.configure(2) do |config|  
  config.vm.define "dhcp" do |dhcp|
    dhcp.vm.box = "ubuntu/trusty64"
    dhcp.vm.hostname = "dhcp"
    dhcp.vm.network "private_network", ip:"10.10.0.4" 
	dhcp.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
	dhcp.vm.provider "virtualbox" do |vb|
	  vb.memory = "2048"  
   end     
	dhcp.vm.provision "shell", inline: <<-SHELL
		sudo apt-get update
# Installation von DHCP Server
        sudo apt-get -y install isc-dhcp-server
# Konfig des Servers
	sudo sed -i 's/example.org/base.dom/g' /etc/dhcp/dhcpd.conf
	sudo sed -i 's/ns2.base.dom/8.8.8.8/g' /etc/dhcp/dhcpd.conf
	sudo sed -i 's/#authoritative/authoritative/g' /etc/dhcp/dhcpd.conf
	sudo sed -i '$asubnet 10.10.0.0 netmask 255.255.255.0 {' /etc/dhcp/dhcpd.conf
	sudo sed -i '$arange 10.10.0.50 10.10.0.90 {' /etc/dhcp/dhcpd.conf
	sudo sed -i '$aoption routers 10.10.0.1;' /etc/dhcp/dhcpd.conf
	sudo sed -i '$a}' /etc/dhcp/dhcpd.conf
	sudo service isc-dhcp-server restart
	sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="ch"/g' /etc/default/locale
SHELL
	end  
 end

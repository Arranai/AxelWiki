In diesem Auftrag ging es darum eine VM mit einem Service automatisiert über Vagrant aufzusetzen.
Als erstes nehmen wir das Vagrantfile auseinander.

Im ersten Teil wird definiert was für ein Betriebssystem verwendet wird und wie die VM heissen soll, ebenfalls können gleich die IP und die Ports eingetragen werden, über welche man die VM nachher erreicht. Zudem gibt man noch an über welche VM Plattform dies laufen wird.
""" Vagrant.configure(2) do |config|  
  config.vm.define "dhcp" do |dhcp|
    dhcp.vm.box = "ubuntu/trusty64"
    dhcp.vm.hostname = "dhcp"
    dhcp.vm.network "private_network", ip:"10.10.0.4" 
	dhcp.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
	dhcp.vm.provider "virtualbox" do |vb|
	  vb.memory = "2048"  
	end """
  

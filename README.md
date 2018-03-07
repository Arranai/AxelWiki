In diesem Auftrag ging es darum eine VM mit einem Service automatisiert über Vagrant aufzusetzen. 
Als erstes nehmen wir das Vagrantfile auseinander.

Im ersten Teil wird definiert was für ein Betriebssystem verwendet wird und wie die VM heissen soll, ebenfalls können gleich die IP und die Ports eingetragen werden, über welche man die VM nachher erreicht. Zudem gibt man noch an über welche VM Plattform dies laufen wird.
```ruby
Vagrant.configure(2) do |config|  
  config.vm.define "dhcp" do |dhcp|
    dhcp.vm.box = "ubuntu/trusty64"
    dhcp.vm.hostname = "dhcp"
    dhcp.vm.network "private_network", ip:"10.10.0.4" 
	dhcp.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
	dhcp.vm.provider "virtualbox" do |vb|
	  vb.memory = "2048"  
  end
```
Um jetzt den Service zu installieren ruft man direkt die Shell (Commando Zeile) im Vagrant auf und genau gleich wie in der Shell gibt man auch dort die Commands ein. Das öffnen der Shell funktioniert so:
```ruby
dhcp.vm.provision "shell", inline: <<-SHELL
```
Zunächst geht es weiter mit dem installieren des Services. Dies wird ganz herkömmlich mit dem ``` apt-get install``` Command. um jegliche Fragen zu überspringen gibt man noch ```-y```ein.
```ruby
sudo apt-get update
sudo apt-get -y install isc-dhcp-server
```
Die Konfiguration des services muss natürlich auch noch gemacht werden. 
```ruby
 sudo sed -i 's/example.org/labor.local/g' /etc/dhcp/dhcpd.conf
 sudo sed -i 's/ns2.labor.local/8.8.8.8/g' /etc/dhcp/dhcpd.conf
 sudo sed -i 's/#authoritative/authoritative/g' /etc/dhcp/dhcpd.conf
 sudo sed -i '$asubnet 10.10.0.0 netmask 255.255.255.0 {' /etc/dhcp/dhcpd.conf 
 sudo sed -i '$arange 10.10.0.50 10.10.0.90 {' /etc/dhcp/dhcpd.conf
 sudo sed -i '$aoption routers 10.10.0.1;' /etc/dhcp/dhcpd.conf
 sudo sed -i '$a}' /etc/dhcp/dhcpd.conf
 sudo service isc-dhcp-server restart
 sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="ch"/g' /etc/default/locale
 ```
 

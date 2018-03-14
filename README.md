# Definition der Kommandos
In diesem Auftrag ging es darum eine VM mit einem Service automatisiert über Vagrant aufzusetzen. 
Als erstes nehmen wir das Vagrantfile auseinander.

## VM Setup
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
## Service
Um jetzt den Service zu installieren ruft man direkt die Shell (Commando Zeile) im Vagrant auf und genau gleich wie in der Shell gibt man auch dort die Commands ein. Das öffnen der Shell funktioniert so:
```ruby
dhcp.vm.provision "shell", inline: <<-SHELL
```
Zunächst geht es weiter mit dem installieren des Services. Dies wird ganz herkömmlich mit dem ``` apt-get install``` Command. um jegliche Fragen zu überspringen gibt man noch ```-y```ein.
```ruby
sudo apt-get update
sudo apt-get -y install isc-dhcp-server
```
Die Konfiguration des services muss natürlich auch noch gemacht werden. Das DHCP Konfigfile wird hier im /etc/dhcp/ abgelegt mit dem Namen dhcpd.conf
```ruby
sudo sed -i 's/example.org/labor.local/g' /etc/dhcp/dhcpd.conf
 ```
In diesem File befindet sich der Domainname, der DHCP Scope, also die Range die vergeben werden darf und der DNS Server.
Der Name der Domain lautet base.dom, zusätzlich wurde noch ein DNS Server angegeben, in diesem Fall der Standard von Google (8.8.8.8)
```ruby
sudo sed -i 's/example.org/base.dom/g' /etc/dhcp/dhcpd.conf
sudo sed -i 's/ns2.base.dom/8.8.8.8/g' /etc/dhcp/dhcpd.conf
 ```
Die IP konfig baut auf, auf einem 10.10.0.1/24 Netz, davon werden die Adressen im Bereich von 10.10.0.10 - 10.10.0.100 verteilt, der Rest gilt als Reserve, kann aber natürlich auch verwendet werden.
```ruby
sudo sed -i '$asubnet 10.10.0.0 netmask 255.255.255.0 {' /etc/dhcp/dhcpd.conf  
sudo sed -i '$arange 10.10.0.10 10.10.0.100 {' /etc/dhcp/dhcpd.conf
```
Um mit Geräten im Netz kommunizieren zu können braucht es eine Gateway Adresse, welche auf das nächste Gerät im Netz verweist, in diesem Fall ein Router mit der Adresse 10.10.0.1
```ruby
sudo sed -i '$aoption routers 10.10.0.1;' /etc/dhcp/dhcpd.conf
```
Danach wird die Konfiguration abgeschlossen und der Service wird neugestartet.
```ruby  
sudo sed -i '$a}' /etc/dhcp/dhcpd.conf
sudo service isc-dhcp-server restart
```
Zum Schluss wird das Tastatur Layout der Maschiene noch auf Schweiz eingestellt.
```ruby
sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="ch"/g' /etc/default/locale
```
## Firewall Service
Den Service ladet man auch wieder mit dem ganz normal installations Befehl herunter, danach wird er gleich aktiviert und der Port 22 wird aufgeschalten, damit Verbindungen mit SSH funktionieren.
```ruby
sudo apt-get install ufw gufw 
sudo ufw enable
sudo ufw allow 22/tcp
```
## Installieren der VM
Um das ganze aufzusetzen einfach in den richtigen Ordner gehen, indem das Vagrantfile abgelegt ist und dieses Kommando ausführen:
```ruby
vagrant up
```

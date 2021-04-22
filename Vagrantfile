Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
end

---------------------------------------
$script = <<-SCRIPT
sudo apt update
sudo apt upgrade -y
SCRIPT
Vagrant.configure("2") do |config|
  config.vm.box = "ktr/mininet"  
  config.vm.provision "shell", inline: $script
end

-----------------------------------------------

Vi Vagrantfile





Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = 'jenkins-local'
  config.vm.provider "virtualbox" do |v|
	v.name = 'jenkins-local'
	v.memory = 2048
  end
  config.vm.network "public_network",
	use_dhcp_assigned_default_route: true
  config.vm.network "private_network", ip: "192.168.56.10"
  # please check that private ip interface exit’s are not with that ip(192.168.56.1)
  config.vm.provision "shell", inline: <<-SHELL
	yum update -y
  SHELL
end


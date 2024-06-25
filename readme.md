# vagrant setup

# install latest virtual box and vagrant from official websit

# if it is not working may be incompatible issue so unistall both of them restart windows machine then reinstall latest versions both of them


# after install update it

vagrant plugin update

# multiple networking

#example

Vagrant.configure("2") do |config|
  # Base box
  config.vm.box = "ubuntu/bionic64"

  # Configure the first network interface (NAT)
  config.vm.network "private_network", type: "dhcp"

  # Configure the second network interface (Host-Only)
  config.vm.network "private_network", type: "static", ip: "192.168.56.10"

  # Configure the third network interface (Bridged)
  config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"

  # Provisioning script (optional)
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2
  SHELL
end

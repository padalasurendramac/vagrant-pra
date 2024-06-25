# vagrant up for below vagrantfile

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
    sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
	sudo apt-get update
	sudo apt-get install -y docker-ce
	sudo systemctl start docker
	sudo systemctl enable docker
	sudo usermod -aG docker ubuntu
	sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
	sudo chmod +x /usr/local/bin/docker-compose
	docker run -p 8080:8080 -p 50000:50000 -d -v /var/run/docker.sock:/var/run/docker.sock -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
  SHELL
end
---


then enable 8080 and 5000 at nat interface at virtualbox

![image](https://github.com/padalasurendramac/vagrant-pra/assets/53860717/a9c37c4b-84a5-43e7-a911-cc4ac3a79b2a)

# load localhot:8080 url
# grep password default password at docker logs <container>



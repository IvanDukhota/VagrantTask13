# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_deps = <<-'SHELL'
sudo apt-get update -y
sudo apt-get install -y openjdk-17-jdk
SHELL

Vagrant.configure("2") do |config|

	config.vm.box = "ubuntu/jammy64"

	config.vm.network "private_network", ip: "192.168.100.100"

	config.vm.provider "virtualbox" do |vb|
		vb.cpus = 2
		vb.memory = 4096
	end

	config.vm.provision "shell", inline: $install_deps

	config.trigger.after :up do |t|
		t.info = "Starting Spring Boot application via Gradle in VM."
		t.run = {
			inline: 'vagrant ssh -c "cd /vagrant && ./gradlew bootRun"'
		}
	end
end

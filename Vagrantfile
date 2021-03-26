Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo This a local DEV environment with NGINX and docker ..."


   Dir.mkdir(ENV['HOME'] + "/.aws") unless Dir.exist?(ENV['HOME'] + "/.aws")
   config.vm.synced_folder ENV['HOME'] + "/.aws", "/home/vagrant/.aws"

  config.vm.define "swarm" do |swarm|
    swarm.vm.network "private_network", ip: "192.168.65.200"
    swarm.vm.network "private_network", ip: "192.168.65.201"
    swarm.vm.network "private_network", ip: "192.168.65.202"
    swarm.vm.network "private_network", ip: "192.168.65.203"
    swarm.vm.network "private_network", ip: "192.168.65.204"
    swarm.vm.network "private_network", ip: "192.168.65.205"
    swarm.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", mount_options: ["dmode=777", "fmode=700"]
    swarm.vm.box = "damianlewis/ubuntu-18.04-nginx-php"
    swarm.vm.provision "shell", inline: "sudo apt-get update"
    #swarm.vm.provision "shell", inline: "sudo apt install -y docker.io python3-pip"
    #swarm.vm.provision "shell", inline: "sudo gpasswd -a vagrant docker && newgrp docker" # enable non-root docker
    #swarm.vm.provision "shell", inline: "sudo apt install -y zsh git-all curl net-tools iputils-ping awscli"
    swarm.vm.provision "shell", inline: "curl -L \"https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)\" -o /usr/local/bin/docker-compose"
    swarm.vm.provision "shell", inline: "sudo chmod +x /usr/local/bin/docker-compose"
    swarm.vm.provision "shell", inline: "curl -sLf https://spacevim.org/install.sh | bash"
    swarm.vm.provision "shell", inline: "sudo chsh -s /usr/bin/zsh vagrant"
  end
end

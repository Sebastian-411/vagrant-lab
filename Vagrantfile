Vagrant.configure("2") do |config|
  # Usar una box de Ubuntu 18.04
  config.vm.box = "ubuntu/bionic64"

  # Configurar la red para acceder al servidor web
  config.vm.network "private_network", type: "dhcp"

  # Provisión para instalar Apache
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2
  SHELL

  # Configurar la carpeta sincronizada
  config.vm.synced_folder ".", "/var/www/html"

  # Configurar la máquina virtual
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
end
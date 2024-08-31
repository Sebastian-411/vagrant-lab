# 📝 Informe de Prácticas: Despliegue de Servidor Web con Vagrant

## 🎯 Objetivo
El objetivo de esta práctica es desplegar un servidor web en un entorno virtual utilizando Vagrant. Configuraremos una máquina virtual con Ubuntu 18.04 y Apache, y demostraremos cómo acceder al servidor web mediante una red privada configurada con DHCP.

## 🔧 Procedimiento

## 1. 🚀 Inicialización del Entorno

- **Comando:** `vagrant init`
  
  Este comando inicializa un nuevo entorno de Vagrant en el directorio actual. Si es la primera vez que se ejecuta Vagrant en este proyecto, se creará un archivo `Vagrantfile` por defecto. 

- **Nota:** En este caso, ya se proporciona un `Vagrantfile` configurado, por lo que este paso solo es necesario si no se ha configurado previamente.

## 2. 🛠️ Configuración del Vagrantfile

Aquí está el contenido del archivo `Vagrantfile`, que define la configuración de la máquina virtual:

```ruby
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
```

- **🔍 Descripción del `Vagrantfile`**:
  - Se utiliza la imagen base de Ubuntu 18.04 (`ubuntu/bionic64`).
  - Configuración de una red privada usando DHCP para facilitar el acceso al servidor.
  - Instalación automática de Apache durante el aprovisionamiento de la VM mediante una provisión de shell.
  - Sincronización de la carpeta actual con el directorio `/var/www/html` dentro de la VM, para un desarrollo web sencillo.
  - Configuración de la máquina virtual con 1024 MB de memoria RAM.

## 3. 🏃‍♂️ Iniciar la Máquina Virtual

- **Comando:** `vagrant up`
  
  Este comando descarga la imagen base si no está disponible y levanta la máquina virtual según la configuración especificada en el `Vagrantfile`.

## 4. 🔑 Acceso a la Máquina Virtual

- **Comando:** `vagrant ssh -c "hostname -I"`
  
  Se accede a la máquina virtual y se obtiene la dirección IP asignada por DHCP. Esto nos permite confirmar la conectividad y acceder a los servicios desplegados en la máquina virtual.

## 5. 🌐 Verificación del Despliegue del Servidor

- **Acción:** Acceder a la IP pública proporcionada para confirmar que el servidor Apache se ha desplegado correctamente.
  
  Una vez obtenida la IP, abre un navegador web y escribe la dirección IP. Si todo ha salido bien, deberías ver la página de inicio predeterminada de Apache, ¡indicando que el servidor está en funcionamiento! 🎉

## ✅ Conclusión
A través de estos sencillos pasos, hemos aprendido cómo configurar y desplegar un servidor web Apache utilizando Vagrant en un entorno virtualizado con Ubuntu 18.04. La práctica incluyó:

1. La inicialización del entorno con Vagrant.
2. La configuración detallada del archivo `Vagrantfile`.
3. El inicio y acceso a la máquina virtual.
4. La verificación del despliegue del servidor web.

Con estos conocimientos, ahora puedes desplegar y gestionar servidores de manera rápida y efectiva en entornos de desarrollo virtualizados. ¡Felicitaciones por completar esta práctica! 🚀🎉

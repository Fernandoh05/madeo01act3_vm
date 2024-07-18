# madeo01act3_vm

# Proyecto Vagrant con Apache y PHP

Este proyecto configura un entorno de desarrollo virtualizado usando Vagrant. La máquina virtual provisionada incluye un servidor web Apache y PHP.

## Prerrequisitos

Antes de comenzar, asegúrate de tener instaladas las siguientes herramientas:

1. **Vagrant**: [Descargar e instalar Vagrant](https://www.vagrantup.com/downloads)
2. **VirtualBox**: [Descargar e instalar VirtualBox](https://www.virtualbox.org/)

## Instrucciones

### 1. Clonar el Repositorio

Clona este repositorio en tu máquina local:

```sh
git clone https://github.com/Fernandoh05/madeo01act3_vm.git
cd <NOMBRE_DEL_DIRECTORIO>
```

## Detalles de Configuración

### Vagrantfile

Aquí está el contenido del `Vagrantfile` usado para este proyecto:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 600
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder ".", "/var/www/html"
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apache2 php libapache2-mod-php
    systemctl enable apache2
    systemctl start apache2
  SHELL
end
```

Este archivo configura una máquina virtual Ubuntu con los siguientes ajustes:
- Caja base: `ubuntu/bionic64`
- Tiempo de espera de arranque: 600 segundos
- Reenvío de puerto: 80 (guest) a 8080 (host)
- Red privada: IP `192.168.33.10`
- Carpeta sincronizada: directorio del proyecto con `/var/www/html` en la VM
- Proveedor de VirtualBox con 1024 MB de memoria
- Provisionamiento: instalación de Apache y PHP

---

### 2. Inicializar la Máquina Virtual

Inicia la máquina virtual ejecutando el siguiente comando:

```sh
vagrant up
```

Este comando hará lo siguiente:
- Descargar la caja base `ubuntu/bionic64` si no está disponible localmente.
- Configurar la máquina virtual con 1024 MB de memoria.
- Configurar un puerto de reenvío desde el puerto 80 de la VM al puerto 8080 de tu máquina host.
- Configurar una red privada con la IP `192.168.33.10` o cualquier otra que desees configurar.
- Sincronizar el directorio del proyecto con `/var/www/html` en la VM.
- Provisionar la máquina para instalar Apache y PHP.

### 3. Acceder a la Máquina Virtual

Una vez que la máquina virtual esté en funcionamiento, puedes acceder a ella a través de SSH con el siguiente comando:

```sh
vagrant ssh
```

### 4. Acceder a la Página PHP

En tu navegador web, navega a `http://localhost:8080` para ver la página PHP.

### 5. Detener la Máquina Virtual

Para detener la máquina virtual, usa el siguiente comando:

```sh
vagrant halt
```

### 6. Destruir la Máquina Virtual

Si deseas eliminar la máquina virtual, usa el siguiente comando:

```sh
vagrant destroy
```

## Contribuidores

| Nombre                         | Correo                              |
|--------------------------------|-------------------------------------|
| Juan Carlos Perez Hernandez    | [jc.przhdz@gmail.com](mailto:jc.przhdz@gmail.com) |
| Fernando Hernandez             | [fernandoh05@outlook.com](mailto:fernandoh05@outlook.com) |
| Eduardo José Gil Apastillar    | [eduardojgila@gmail.com](mailto:eduardojgila@gmail.com) |
---
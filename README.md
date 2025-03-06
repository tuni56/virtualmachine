# Guía Detallada: Ubuntu en VM, Python Virtual Env y PostgreSQL en Windows 11

Si necesitas trabajar con Ubuntu, gestionar entornos virtuales de Python y usar PostgreSQL en Windows 11, esta guía te ayudará a configurarlo paso a paso.

## 1️⃣ Crear una Máquina Virtual Ubuntu con VirtualBox y Vagrant

### 🛠 Requisitos Previos:
- [Descargar e instalar VirtualBox](https://www.virtualbox.org/)
- [Descargar e instalar Vagrant](https://developer.hashicorp.com/vagrant/downloads)

### 🚀 Pasos de Instalación:
1. **Crear una carpeta para el proyecto:**
   ```sh
   mkdir ubuntu-vm && cd ubuntu-vm
   ```
2. **Inicializar un archivo Vagrantfile:**
   ```sh
   vagrant init ubuntu/focal64
   ```
3. **Editar el `Vagrantfile`** para configurar la VM:
   ```ruby
   Vagrant.configure("2") do |config|
     config.vm.box = "ubuntu/focal64"
     config.vm.network "private_network", type: "dhcp"
     config.vm.provider "virtualbox" do |vb|
       vb.memory = "2048"
       vb.cpus = 2
     end
   end
   ```
4. **Levantar la VM:**
   ```sh
   vagrant up
   ```
5. **Acceder a la VM:**
   ```sh
   vagrant ssh
   ```

## 2️⃣ Configurar Python con pyenv y virtualenv

### 🛠 Requisitos Previos:
- Tener la VM Ubuntu en funcionamiento
- Tener `git`, `curl` y `build-essential` instalados:
  ```sh
  sudo apt update && sudo apt install -y git curl build-essential
  ```

### 🚀 Instalación de pyenv y virtualenv:
1. **Instalar pyenv:**
   ```sh
   curl https://pyenv.run | bash
   ```
   Agregar estas líneas al final de `~/.bashrc`:
   ```sh
   export PATH="$HOME/.pyenv/bin:$PATH"
   eval "$(pyenv init --path)"
   eval "$(pyenv virtualenv-init -)"
   ```
   Luego, recargar la configuración:
   ```sh
   source ~/.bashrc
   ```
2. **Instalar una versión de Python y configurarla:**
   ```sh
   pyenv install 3.10.6
   pyenv global 3.10.6
   ```
3. **Crear un entorno virtual:**
   ```sh
   pyenv virtualenv 3.10.6 myenv
   pyenv activate myenv
   ```

## 3️⃣ Instalar PostgreSQL en WSL y Conectarlo con Windows

### 🛠 Requisitos Previos:
- Tener habilitado el **Subsistema de Windows para Linux (WSL2)**
- Instalar Ubuntu desde la Microsoft Store

### 🚀 Instalación de PostgreSQL en WSL:
1. **Abrir Ubuntu en Windows y actualizar paquetes:**
   ```sh
   sudo apt update && sudo apt upgrade -y
   ```
2. **Instalar PostgreSQL:**
   ```sh
   sudo apt install -y postgresql postgresql-contrib
   ```
3. **Iniciar el servicio PostgreSQL:**
   ```sh
   sudo service postgresql start
   ```
4. **Acceder a la base de datos como usuario `postgres`:**
   ```sh
   sudo -i -u postgres
   psql
   ```
   Para salir de PostgreSQL, escribe `\q`.

### 🎯 Conectar PostgreSQL desde Windows:
1. **Obtener la IP de WSL:**
   ```sh
   ip addr show eth0 | grep "inet " | awk '{print $2}' | cut -d'/' -f1
   ```
2. **Permitir conexiones remotas en PostgreSQL:**
   ```sh
   sudo nano /etc/postgresql/14/main/postgresql.conf
   ```
   Cambiar esta línea:
   ```sh
   listen_addresses = '*'
   ```
3. **Configurar acceso desde Windows:**
   ```sh
   sudo nano /etc/postgresql/14/main/pg_hba.conf
   ```
   Agregar al final:
   ```sh
   host    all             all             0.0.0.0/0               md5
   ```
4. **Reiniciar PostgreSQL:**
   ```sh
   sudo service postgresql restart
   ```
5. **Conectar desde Windows con un cliente PostgreSQL (pgAdmin, DBeaver, etc.)** usando la IP de WSL y el puerto `5432`.

---

🎉 **¡Listo! Ahora tienes un entorno de desarrollo completo con Ubuntu, Python y PostgreSQL en Windows 11.** Si esta guía te ayudó, ¡compártela con otros! 🚀
    ** No olvides darle una estrellita al repositorio!

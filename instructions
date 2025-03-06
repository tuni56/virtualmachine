# Detailed Guide: Ubuntu VM, Python Virtual Env, and PostgreSQL on Windows 11

If you need to work with Ubuntu, manage Python virtual environments, and use PostgreSQL on Windows 11, this guide will help you set it up step by step.

## 1️⃣ Create an Ubuntu Virtual Machine with VirtualBox and Vagrant

### 🛠 Prerequisites:
- [Download and install VirtualBox](https://www.virtualbox.org/)
- [Download and install Vagrant](https://developer.hashicorp.com/vagrant/downloads)

### 🚀 Installation Steps:
1. **Create a project folder:**
   ```sh
   mkdir ubuntu-vm && cd ubuntu-vm
   ```
2. **Initialize a Vagrantfile:**
   ```sh
   vagrant init ubuntu/focal64
   ```
3. **Edit the `Vagrantfile`** to configure the VM:
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
4. **Start the VM:**
   ```sh
   vagrant up
   ```
5. **Access the VM:**
   ```sh
   vagrant ssh
   ```

## 2️⃣ Set Up Python with pyenv and virtualenv

### 🛠 Prerequisites:
- Have the Ubuntu VM running
- Install `git`, `curl`, and `build-essential`:
  ```sh
  sudo apt update && sudo apt install -y git curl build-essential
  ```

### 🚀 Install pyenv and virtualenv:
1. **Install pyenv:**
   ```sh
   curl https://pyenv.run | bash
   ```
   Add these lines at the end of `~/.bashrc`:
   ```sh
   export PATH="$HOME/.pyenv/bin:$PATH"
   eval "$(pyenv init --path)"
   eval "$(pyenv virtualenv-init -)"
   ```
   Then, reload the configuration:
   ```sh
   source ~/.bashrc
   ```
2. **Install a Python version and set it up:**
   ```sh
   pyenv install 3.10.6
   pyenv global 3.10.6
   ```
3. **Create a virtual environment:**
   ```sh
   pyenv virtualenv 3.10.6 myenv
   pyenv activate myenv
   ```

## 3️⃣ Install PostgreSQL on WSL and Connect it with Windows

### 🛠 Prerequisites:
- Enable **Windows Subsystem for Linux (WSL2)**
- Install Ubuntu from the Microsoft Store

### 🚀 Install PostgreSQL on WSL:
1. **Open Ubuntu on Windows and update packages:**
   ```sh
   sudo apt update && sudo apt upgrade -y
   ```
2. **Install PostgreSQL:**
   ```sh
   sudo apt install -y postgresql postgresql-contrib
   ```
3. **Start the PostgreSQL service:**
   ```sh
   sudo service postgresql start
   ```
4. **Access the database as the `postgres` user:**
   ```sh
   sudo -i -u postgres
   psql
   ```
   To exit PostgreSQL, type `\q`.

### 🎯 Connect PostgreSQL from Windows:
1. **Get the WSL IP address:**
   ```sh
   ip addr show eth0 | grep "inet " | awk '{print $2}' | cut -d'/' -f1
   ```
2. **Allow remote connections in PostgreSQL:**
   ```sh
   sudo nano /etc/postgresql/14/main/postgresql.conf
   ```
   Change this line:
   ```sh
   listen_addresses = '*'
   ```
3. **Configure access from Windows:**
   ```sh
   sudo nano /etc/postgresql/14/main/pg_hba.conf
   ```
   Add at the end:
   ```sh
   host    all             all             0.0.0.0/0               md5
   ```
4. **Restart PostgreSQL:**
   ```sh
   sudo service postgresql restart
   ```
5. **Connect from Windows using a PostgreSQL client (pgAdmin, DBeaver, etc.)** with the WSL IP and port `5432`.

---

🎉 **Done! Now you have a complete development environment with Ubuntu, Python, and PostgreSQL on Windows 11.** If this guide helped you, share it with others! 🚀


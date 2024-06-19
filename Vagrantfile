# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|
    #Configuração Geral da VM Vangrant
    # config.vm.box = "geerlingguy/oraclelinux88"
    config.vm.box_download_insecure = true
    config.ssh.insert_key = false
    config.vbguest.auto_update = true
    config.vm.boot_timeout = 600
    config.vm.synced_folder ".", "/vagrant", disabled: false  
    config.vm.provider :virtualbox do |v|
       v.memory = 1024
       v.cpus = 1
       #v.linked_clone = true
    end
    # Servidor Ansible
    config.vm.define "ansible" do |ansible|
        ansible.vm.hostname = "ansible-srv.lan"
        ansible.vm.box = "oraclebase/oracle-8"
        ansible.vm.network :private_network, ip: "192.168.56.100", netmask:"255.255.255.0"
        ansible.vm.network :forwarded_port, guest: 22, host: 2250, id: 'ssh'
        #ansible.vm.synced_folder "C:/Users/adelmo.silva/Desktop/App_Oracle/", "/ora-bins", disabled: false
        ansible.vm.provider :virtualbox do |v|
            v.memory = 4096
            v.cpus = 2
            v.name= "Target-Ansible"
        end
    end
                
    # Servidor Webserver
    config.vm.define "webserver" do |webserver|
        webserver.vm.hostname = "webserver-srv.lan"
        webserver.vm.box = "debian/contrib-buster64"
        webserver.vm.network :private_network, ip: "192.168.56.106", netmask:"255.255.255.0"
        webserver.vm.network :forwarded_port, guest: 22, host: 2251, id: 'ssh'
        webserver.vm.provider :virtualbox do |v|
            v.memory = 1024
            v.cpus = 1
            v.name= "Target-WebServer"
        end
    end
    
    # Servidor NFS
    config.vm.define "nfs" do |nfs|
        nfs.vm.box = "oraclebase/oracle-8"
        nfs.vm.hostname = "nfs-srv.lan"
        nfs.vm.network :private_network, ip: "192.168.56.104", netmask:"255.255.255.0"
        nfs.vm.network :forwarded_port, guest: 22, host: 2253, id: 'ssh'
        #nfs.vm.synced_folder "C:/Users/adelmo.silva/Desktop/App_Oracle/", "/ora-bins", disabled: false
        nfs.vm.provider :virtualbox do |v|
            v.memory = 4096
            v.cpus = 2
            v.name= "Target-NFS"
        end
    end

    # Servidor NGINX
    config.vm.define "nginx" do |nginx|
        nginx.vm.hostname = "nginx-srv.lan"
        nginx.vm.box = "debian/contrib-buster64"
        nginx.vm.network :private_network, ip: "192.168.56.102", netmask:"255.255.255.0"
        nginx.vm.network :forwarded_port, guest: 22, host: 2252, id: 'ssh'
        nginx.vm.provider :virtualbox do |v|
            v.memory = 1024
            v.cpus = 1
            v.name= "Target-NGINX"
        end
    end
    
    # VM Windows Server 2016
     config.vm.define "windows2016" do |windows2016|
        windows2016.vm.box = "jborean93/WindowsServer2016"
        windows2016.vm.hostname = "srvwindows2016-lan"
        windows2016.vm.network :private_network, ip: "192.168.56.103", netmask:"255.255.255.0", guest:270018, host: 27018
        windows2016.vm.provider :virtualbox do |v|
            v.memory = 2048
            v.cpus = 2
            v.name= "Target-WindowsServer2016"
            #v.linked_clone = true
        
        end
    end   
end
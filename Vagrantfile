# -*- mode: ruby -*-
# vi: set ft=ruby :

#Trabalho de Administração de Redes de Computadores
#Aluno: Luis Gabriel Queiroz Carrijo

Vagrant.configure("2") do |config|
    config.vm.define "vm1" do |vm1|
        vm1.vm.box = "gusztavvargadr/ubuntu-server"  
        vm1.vm.network "private_network", ip: "192.168.1.10"
        vm1.vm.network "forward_port": guest:80 host:8080
        vm1.vm.network "forward_port": guest:81 host:8081
        vm1.vm.network "forward_port": guest:82 host:8082
        vm1.vm.network "forward_port": guest:83 host:8083
        vm1.vm.network "forward_port": guest:84 host:8084
        vm1.vm.synced_folder ".", "/dirCompartilhado"
        vm1.vm.provider "virtualbox" do |vb|
            vb.name = "VM1"
            vb.memory = "1024"
        end
        
        #Conferir a documentação de cada um
        vm1.vm.provision "shell",inline: <<-SHELL 
            sudo apt update
            sudo apt install docker.io -y
            docker run -d --name containerWEB -v /dirCompartilhado:/usr/local/apache2/htdocs/ -p 80:80 httpd
            docker run -d --name containerDNS -v /dirCompartilhado:/etc/bind/named.conf -p 81:53 ubuntu/bind9
            docker run -d --name containerNFS -v /dirCompartilhado:/nfsshare -p 82:2049 itsthenetwork/nfs-server-alpine
            docker run -d --name containerFTP -v /dirCompartilhado:/home/vsftpd -p 83: ustclug/ftp
            docker run -d --name containerDHCP -v  -p 84:80 networkboot/dhcpd
        SHELL
    end
end

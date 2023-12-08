# -*- mode: ruby -*-
# vi: set ft=ruby :

#Trabalho de Administração de Redes de Computadores
#Aluno: Luis Gabriel Queiroz Carrijo

Vagrant.configure("2") do |config|
    config.vm.define "vm1" do |vm1|
        vm1.vm.box = "gusztavvargadr/ubuntu-server"  
        vm1.vm.network "private_network", ip: "192.168.1.10", gateway: "192.168.1.11"
        vm1.vm.network "forwarded_port", guest:80, host:9080
        vm1.vm.network "forwarded_port", guest:81, host:9081
        vm1.vm.network "forwarded_port", guest:82, host:9082
        vm1.vm.network "forwarded_port", guest:83, host:9083
        vm1.vm.network "forwarded_port", guest:84, host:9084
        config.vm.network "public_network", type: "dhcp", bridge: "wlp3s0"
        config.vm.synced_folder ".", "/dirCompartilhado"
        vm1.vm.provider "virtualbox" do |vb|
            vb.name = "VM1"
            vb.memory = "1024"
        end
        
        #Conferir a documentação de cada um
        vm1.vm.provision "shell",inline: <<-SHELL 
            sudo sysctl -w net.ipv4.ip_forward=1
            sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
            sudo apt update
            sudo apt install docker.io -y
            sudo docker pull httpd
            sudo docker pull ubuntu/bind9
            sudo docker pull itsthenetwork/nfs-server-alpine
            sudo docker pull ustclug/ftp
            sudo docker pull networkboot/dhcpd
            docker run -d --name containerWEB -v /dirCompartilhado/Web:/usr/local/apache2/htdocs/ -p 80:80 httpd # Pronto
            docker run -d --name containerDNS -v /dirCompartilhado/DNS/named.conf:/etc/bind/named.conf -v /dirCompartilhado/DNS/cache:/var/cache/bind -v /dirCompartilhado/DNS/records:/var/lib/bind -e TZ=UTC -p 81:53 ubuntu/bind9
            docker run -d --name containerNFS --privileged -v /dirCompartilhado/NFS:/nfsshare -p 82:2049 -e SHARED_DIRECTORY=/nfsshare itsthenetwork/nfs-server-alpine:latest
            docker run -d --name containerFTP -itd --restart=always -p 83:22 -p 84:40000 -v /dirCompartilhado/FTP/data:/srv/ftp -v /dirCompartilhado/FTP/log:/var/log -v /dirCompartilhado/FTP/home:/home -e PRIVATE_PASSWD=123456789 -e PASV_ADDRESS=127.0.0.1 ustclug/ftp
            docker run -d --name containerDHCP -it --rm --init --net=host -v /dirCompartilhado/DHCP/data:/data networkboot/dhcpd eth0
        SHELL
    end

    config.vm.define "vm2" do |vm2|
        vm2.vm.box = "gusztavvargadr/ubuntu-server"  
        config.vm.network "private_network", ip: "192.168.1.12", gateway: "192.168.1.13"
        vm2.vm.provider "virtualbox" do |vb|
            vb.name = "VM2"
            vb.memory = "1024"
        end
    end
end

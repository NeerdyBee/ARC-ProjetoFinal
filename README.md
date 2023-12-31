# ARC-ProjetoFinal

# DOCUMENTAÇÃO: Projeto de rede empresarial, implantação e gerenciamento utilizando Linux, Vagrant e Docker.

# AUTORES: Ramiro Vieira de Moura, Luis Gabriel Queiroz Carrijo

#Introdução: O seguinte repositório tem como objetivo projetar, implementar e gerenciar uma rede empresarial utilizando Linux, com foco nos serviços essenciais como DHCP, DNS, Web, FTP, NFS, e virtualização utilizando Vagrant e Docker. Nossa infraestrutura pretende garantir a eficiência, escalabilidade e segurança para as operações de uma empresa.


# 1. Topologia da Rede:
Neste projeto de criação de uma rede empresarial, iremos utilizar a topologia em estrela devido a sua simplicidade de design que ajudará a melhorar a escalabilidade da rede.
Servidores e serviços essenciais vão estar presentes no núcleo da rede, enquanto máquinas virtuais e contêineres serão distribuídos em suas extremidades.

# 2. Segmentação das Sub-Redes: 
Sub-rede para Servidores (ex: 192.168.1.0/24)
Sub-rede para Máquinas Virtuais (ex: 192.168.2.0/24)
Sub-rede para Contêineres Docker (ex: 192.168.3.0/24)

# As configurações das VMs:

1. VM1 - Servidor de Serviços
- Sistema Operacional: Ubuntu Server 20.04 LTS
- Interface de Rede 1 (eth0): IP Privado Estático (192.168.1.10)
- Funções:
  - Servidor DHCP;
  - Servidor DNS;
  - Servidor WEB (Apache);
  - Servidor FTP
  - Servidor NFS
- Pasta Compartilhada: `/var/www/html` na máquina host deve ser compartilhada com `/var/www/html` na VM1.

2. VM2 - Cliente 
- Sistema Operacional: Ubuntu Server 20.04 LTS
- Interface de Rede 1 (eth0): IP Privado Estático (192.168.2.10)
- Função: Conectar e verificar as funcionalidades dos serviços do servidor

# 3. Pré-requisitos de instalação:
- DHCP (Dynamic Host Configuration Protocol): Será utilizado um servidor DHCP para atribuirmos a dinâmica de endereços IP nas sub-redes.
- DNS (Domain Name System): Será utilizado também um servidor DNS para resolução de nomes internos e externos.
- WEB: Será também implantado um servidor web (Apache) para hospedar aplicativos internos.
- FTP (File Transfer Protocol): Será utilizado essa configuração para transferência de arquivos.
- NFS (Network File System): Será implementado um servidor NFS para compartilhamento de arquivos entre máquinas virtuais.
- Vagrant: Será utilizado para criação e manipulação das máquinas virtuais de acordo com a topologia definida no documento.
- Docker: Será utilizado para empacotar e implantar aplicativos em contêineres isolados.

# 4. Configuração e instalação dos recursos necessários (abra o terminal Linux e digite os comandos para instalação dos recursos)

- Instalação Vagrant (utilizado para criar Scripts para então criação das máquinas virtuais de acordo com as especificações desejadas.)
Digite:

$sudo apt update
$sudo apt install vagrant -y

- Instalação Docker (utilizado para construir imagens e composição de containers)

$sudo apt update

$sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

$echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

$sudo apt update

$sudo apt install docker-ce docker-ce-cli containerd.io -y

- Docker Compose (utilizado para realizar a comunicação entre os contêineres.)

$sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$sudo chmod +x /usr/local/bin/docker-compose

# Após terminar a instalação verifique os arquivos:

$vagrant --version

$docker --version

$docker-compose --version



# 5. Recursos de  dos serviços: (DHCP, DNS, Web, FTP, NFS.)
-DHCP: https://hub.docker.com/r/networkboot/dhcpd
-DNS: https://hub.docker.com/r/ubuntu/bind9
-WEB: https://hub.docker.com/_/httpd 
-FTP: https://hub.docker.com/r/ustclug/ftp
-NFS: https://hub.docker.com/r/itsthenetwork/nfs-server-alpine



# 6. Instruções para seu Uso e Testes de serviços
   1. Clone o repositório em sua máquina.
   
   bash
     git clone <URL-do-repositório>
     cd <nome-do-diretório-clonado>
  
   2. Inicie as máquinas virtuais usando o Vagrant. Selecione a pasta e abrindo com terminal e execute o comando "vagrant up".

   3. Confirme sua iniciação utilizando o comando "vagrant status".

   4. Após a criação das VMs, utilize o seguinte comando para se conectar a VM desejada.

   Ex.:
     vagrant ssh <Nome_da_VM>
  
   4. Verifique a conectividade entre as VMs utilizando os endereços IP da rede privada.

   5. Por fim, ao final da execução utilize o VirtualBox para Desligar e Excluir as máquinas virtuais que estão em execução, ou usando o Terminal digite os comando "vagrant halt" para encerrar ou "vagrant destroy".



# 7. Testes Extensivos de todos os serviços (A FAZER)
Verificação de conectividade em todas as sub-redes.
Testes de resolução DNS.
Transferência de arquivos via FTP.
Acesso a aplicativos web internos.
Testes de compartilhamento de arquivos via NFS.

Guia para Testes 

1. Testes de Conectividade:

- Ping:
VM1: ping 192.168.2.10 para verificar a conectividade com VM2.
VM2: ping 192.168.1.10 para verificar a conectividade com VM1.

- SSH:
Acesse VM1 de VM2: ssh 192.168.1.10
Acesse VM2 de VM1: ssh 192.168.2.10

2. Testes de Serviços:

- DHCP: 
Em VM2, verifique se o IP foi atribuído automaticamente pela VM1.

- DNS: 
Em ambas as VMs, use nslookup ou dig para resolver nomes de domínio. Ex: “nslookup google.com”

- Apache (VM1):
Acesse o servidor web de VM2: curl http://192.168.1.10
Coloque um arquivo na pasta compartilhada /var/www/html e verifique se é acessível.

- FTP (VM1):
Em VM2, tente conectar via FTP: ftp 192.168.1.10
Faça upload ou download de um arquivo.

- NFS (VM1):
Em VM2, monte o compartilhamento NFS: sudo mount -t nfs 192.168.1.10:/vagrant/html /mnt/html
Verifique se pode acessar os arquivos no compartilhamento.



# 8. Testes e possíveis Manutenções: (A FAZER)
.
.
.

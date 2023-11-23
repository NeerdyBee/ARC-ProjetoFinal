# ARC-ProjetoFinal

#DOCUMENTAÇÃO: Projeto de rede empresarial, implantação e gerenciamento utilizando Linux, Vagrant e Docker.
#AUTORES: Ramiro Vieira de Moura, Luis Gabriel Carrijo

#Introdução: 
O seguinte projeto abaixo tem como objetivo projetar, implementar e gerenciar uma rede empresarial utilizando Linux, com foco nos serviços essenciais como DHCP, DNS, Web, FTP, NFS, e virtualização utilizando Vagrant e Docker. Nossa infraestrutura pretende garantir a eficiência, escalabilidade e segurança para as operações de uma empresa.


#1. Topologia da Rede:
Neste projeto de criação de uma rede empresarial, iremos utilizar a topologia em estrela devido a sua simplicidade de design que ajudará a melhorar a escalabilidade da rede.
Servidores e serviços essenciais vão estar presentes no núcleo da rede, enquanto máquinas virtuais e contêineres serão distribuídos em suas extremidades.

#2. Segmentação das Sub-Redes: 
Sub-rede para Servidores (ex: 192.168.1.0/24)
Sub-rede para Máquinas Virtuais (ex: 192.168.2.0/24)
Sub-rede para Contêineres Docker (ex: 192.168.3.0/24)

#3. Serviços essenciais a serem implementados:
DHCP (Dynamic Host Configuration Protocol): Será utilizado um servidor DHCP para atribuirmos a dinâmica de endereços IP nas sub-redes.
DNS (Domain Name System): Será utilizado também um servidor DNS para resolução de nomes internos e externos.
WEB: Será também implantado um servidor web (Apache) para hospedar aplicativos internos.
FTP (File Transfer Protocol): Será utilizado essa configuração para transferência de arquivos.
NFS (Network File System): Será implementado um servidor NFS para compartilhamento de arquivos entre máquinas virtuais.
Vagrant: Será utilizado para criação e manipulação das máquinas virtuais de acordo com a topologia definida no documento.
Docker: Será utilizado para empacotar e implantar aplicativos em contêineres isolados.


#4. Configuração e instalação dos recursos necessários: 
Abra o terminal Linux e digite os comandos para instalação dos recursos:

-Instalação Vagrant (utilizado para criar Scripts para então criação das máquinas virtuais de acordo com as especificações desejadas.)
Digite:

$sudo apt update
$sudo apt install vagrant -y

-Instalação Docker (utilizado para construir imagens e composição de containers)

$sudo apt update

$sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

$echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

$sudo apt update

$sudo apt install docker-ce docker-ce-cli containerd.io -y

Docker Compose (utilizado para realizar a comunicação entre os contêineres.)

$sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$sudo chmod +x /usr/local/bin/docker-compose


-Após terminar a instalação verifique os arquivos:

$vagrant --version

$docker --version

$docker-compose --version




#5. Configuração dos serviços: (DHCP, DNS, Web, FTP, NFS.)
-DHCP

-DNS

-WEB

-FTP

-NFS
.
.
.

#6. Testes Extensivos de todos os serviços

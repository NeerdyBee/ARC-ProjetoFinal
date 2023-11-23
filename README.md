# ARC-ProjetoFinal

# DOCUMENTAÇÃO: Projeto de rede empresarial, implantação e gerenciamento utilizando Linux, Vagrant e Docker.

# AUTORES: Ramiro Vieira de Moura, Luis Gabriel Carrijo

#Introdução: O seguinte repositório tem como objetivo projetar, implementar e gerenciar uma rede empresarial utilizando Linux, com foco nos serviços essenciais como DHCP, DNS, Web, FTP, NFS, e virtualização utilizando Vagrant e Docker. Nossa infraestrutura pretende garantir a eficiência, escalabilidade e segurança para as operações de uma empresa.


# 1. Topologia da Rede:
Neste projeto de criação de uma rede empresarial, iremos utilizar a topologia em estrela devido a sua simplicidade de design que ajudará a melhorar a escalabilidade da rede.
Servidores e serviços essenciais vão estar presentes no núcleo da rede, enquanto máquinas virtuais e contêineres serão distribuídos em suas extremidades.

# 2. Segmentação das Sub-Redes: 
Sub-rede para Servidores (ex: 192.168.1.0/24)
Sub-rede para Máquinas Virtuais (ex: 192.168.2.0/24)
Sub-rede para Contêineres Docker (ex: 192.168.3.0/24)

# 3. Pré-requisitos de instação:

- DHCP (Dynamic Host Configuration Protocol): Será utilizado um servidor DHCP para atribuirmos a dinâmica de endereços IP nas sub-redes.

- DNS (Domain Name System): Será utilizado também um servidor DNS para resolução de nomes internos e externos.

- WEB: Será também implantado um servidor web (Apache) para hospedar aplicativos internos.

- FTP (File Transfer Protocol): Será utilizado essa configuração para transferência de arquivos.

- NFS (Network File System): Será implementado um servidor NFS para compartilhamento de arquivos entre máquinas virtuais.

- Vagrant: Será utilizado para criação e manipulação das máquinas virtuais de acordo com a topologia definida no documento.

- Docker: Será utilizado para empacotar e implantar aplicativos em contêineres isolados.


# 4. Configuração e instalação dos recursos necessários: 
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

# Após terminar a instalação verifique os arquivos:

$vagrant --version

$docker --version

$docker-compose --version



# 5. Configuração dos serviços: (DHCP, DNS, Web, FTP, NFS.)
-DHCP

-DNS

-WEB

-FTP

-NFS
.
.
.

# 6. Testes Extensivos de todos os serviços (utilizar prints)

Verificação de conectividade em todas as sub-redes.
Testes de resolução DNS.
Transferência de arquivos via FTP.
Acesso a aplicativos web internos.
Testes de compartilhamento de arquivos via NFS.


Descrever e documentar os resultados dos Testes unitários:

.
.
.

Descrever caso houver as Correções feitas e ajustes necessários: (Mencionando as versões dos testes, ex 1.0, 2.0)

.
.
.


# 7. Entrega final e possíveis Manutenções:

Entrega Final:

.
.
.

Arquivos de configuração, scripts e documentação.
Instruções claras para reproduzir a configuração desde a instalação dos programas necessários para execução.

Manutenção Prevista:

.
.
.

Procedimentos de manutenção e atualização.
Projetos com uma infraestrutura de rede robusta e altamente escalável, utilizando tecnologias Linux, Vagrant e Docker. Necessitam de uma documentação abrangente que garantirá a compreensão e a replicabilidade do ambiente implementado.






## Instruções para seu Uso e Testes de serviços (AINDA NÃO DEFINIDO AS VMS)

1. Clone o repositório “Nomedorepositorio” em sua máquina.
   
bash
  git clone <URL-do-repositório>
  cd <nome-do-diretório-clonado>
  
2. Inicie as máquinas virtuais usando o Vagrant.
selecione a pasta e abrindo com terminal e de um vagrant up.

3. Após a criação das VMs, utilize o seguinte comando para se conectar a VM desejada.

Ex   
  vagrant ssh VM1
  vagrant ssh VM2
  vagrant ssg VM3
  
3. Verifique a conectividade entre as VMs utilizando os endereços IP da rede
privada.

4. Verifique se as VMs tem conectividade com a Internet executando o comando ‘ping
google.com’ dentro de uma delas.

5. Teste os serviços (Apache, MySQL) nas VMs para garantir que estão funcionando
de acordo.

  - Para testar o Apache: Exemplo curl http://192.168.56.10

  - Para testar o MySQL VM2: Exemplo telnet 192.168.56.11 3306

8. Por fim, ao final da execução utilize o VirtualBox para Desligar e Excluir as máquinas virtuais que estão em execução.



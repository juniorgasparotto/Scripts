* Logar como root na máquina (use exit caso tenha logado com outro usuário)
* Atribuir os usuários como root (/centOS/add-user-as-sudo)
* Sair do root e logar com o usuário
* Se passar por root (sudo su)
* Setar ip fixo (/centOS/ip-static)
* Instalar openshift (/openshift/install/ansible-all-in-one/install)
* Configurar o /etc/docker/daemon.json do docker para dar acesso a internet ao usar "docker build" e etc (/docker/configure-daemon.json)
* Configurar as métricas do HPA (/openshift/commands/enable-metrics-hpa)
* Configurar as métricas (/openshift/commands/enable-metrics-server)
* Configurar as métricas (/openshift/commands/enable-metrics-monitoring-prometheus)
* Setup do HD de 2TB no diretório "/files" (/centOS/mount-hd)
* Setup Samba do diretório "/files" (/centOS/samba) (usar o root no windows)
* Setup NFS do diretório "/files/registry" (/centOS/nfs)
* Setup NFS para o registry do docker (/openshift/commands/image-change-docker-registry-to-nfs)
  * Criar o secret também para quando subir imagem no registry interno
* ****************** Criar alguns PVs para facilitar a instalação de projetos (20 PV de 10GB) 
* Configurar o S2I para criar imagens via linha de comando
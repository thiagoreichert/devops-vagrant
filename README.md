Projects Infrastructure as Code
-- Author: Thiago Reichert

Instalar Vagrant
Instalar VirtualBox (OBS: Durante a instalação de ser pausado o antivirus, senão o o SO não permite a criação do network pelo VB)
OBS: Avaliar na documentação do Vagrant se há compatibilidade entre versão atual do Vagrant com atual do VirtualBox.

1 - Copiar o arquivo Vagrantfile para um diretório local específico para esta atividade.
2 - No bash acessar o diretório e executar "vagrant up"

Acesso a VM pelo bash local:
vagrant ssh

Acesso a VM pelo IP público:
vagrant ssh-config
ssh -i private_key vagrant@IP_PUB 

Montagem entre host e guest: 
DIR_LOCAL_HOST do Vagrantfile = /vagrant na VM

Comandos úteis:

Status da Máquina:
vagrant up - Liga a VM
vagrant suspend - Suspende a VM
vagrant resume - Ativa a VM suspensa
vagrant halt - Desliga a VM
vagrant reload - Reinicia a VM se alterado o Vagrantfile

Outros comandos:
vagrant ssh-config - Detalhes da configuração de SSH
vagrant list-commands - Lista de comandos

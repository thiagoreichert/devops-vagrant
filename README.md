### Projects Infrastructure as Code -- Author: Thiago Reichert



### Instalação e Configuração

Instalar Vagrant

Instalar VirtualBox 

(OBS: Durante a instalação deve ser pausado o antivírus, senão o o SO não permite a criação do network pelo VB)



1 - Copiar o arquivo Vagrantfile para um diretório local específico para esta atividade.

2 - No bash acessar o diretório e executar "vagrant up" para iniciar as VMs.



### Acessos a VM:

##### Acesso a VM pelo bash local:

```
vagrant ssh
```

##### Acesso a VM pelo IP público:

```
vagrant ssh-config
ssh -i private_key vagrant@IP_PUB
```



### Montagem

Montagem entre host e guest: 

DIR_LOCAL_HOST do Vagrantfile = /vagrant na VM



### Comandos úteis:

##### Status da Máquina:

vagrant status - Status das VMs no diretório atual

vagrant global-status - Status das VMs de todo o host

vagrant up - Liga a VM

vagrant suspend - Suspende a VM

vagrant resume - Ativa a VM suspensa

vagrant halt - Desliga a VM

vagrant reload - Reinicia a VM se alterado o Vagrantfile



##### Outros comandos:

vagrant ssh-config - Detalhes da configuração de SSH

vagrant list-commands - Lista de comandos

vagrant validate - Valida se o arquivo Vagrantfile está com a sintaxe correta.



### Configurações do Vagrantfile

Verificar o arquivo Vagrant Help.
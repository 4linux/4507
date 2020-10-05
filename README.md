PenTest: Técnicas de Intrusão em Redes Corporativas
===================================================

> **"A penatration test is a snapshot of the current security posture."** Lee Allen (Autor de _Advanced Penetration Testing for Highly-Secured Environments_)

Repositório Criado para armazemento de informações gerais do curso de PenTest.

Vagrant
-----------
O [Vagrant](https://www.vagrantup.com/), de forma geral, é uma aplicação de cria e gerencia ambientes virtualizados, baseado em providers (Virtualbox, VMWare, etc) e provisions (Shell, Ansible, Puppet, etc).

Por isso, iremos utiliza-lo para criar a infraestrutura do Laboratório deste curso. E para isso já temos preparado um Vagrantfile, arquivo que contém a infraestrutura baseada em codigo.

* [Vagrantfile](./Vagrantfile)

Este ambiente é contruirá uma máquina com [Kali Linux](https://www.kali.org/) e duas máquinas [Metasploitable3](https://github.com/rapid7/metasploitable3) (Mantida pela Rapid7), sendo uma Linux - Ubuntu 14.04 - e uma Windows Server 2008.

### Procedimento para Inicializar a infraestrutura
```bash
git clone https://github.com/yesquines/PenTest.git pentest_lab
cd pentest_lab
vagrant up
```
> OBS¹: É recomendado no minimo 8Gb RAM para utilização desse Laboratório.

> OBS²: O tamanho das boxes, imagens utilizadas pelo vagrant, são relativamento grandes, sendo assim o procedimento de inicialização pode demorar.

### Vagrant - Comandos Básicos

Comandos     | Descrição
------------ |------------------
vagrant init| Gera o VagrantFile
vagrant box add <box> | Baixar imagem do sistema
vagrant box status    | Verificar o status dos boxes criados
vagrant up            | Cria/Liga as VMs baseado no VagrantFile
vagrant up --provision| Sobe a máquina com as alterações feitas no VagrantFile
vagrant provision     | Provisiona mudanças logicas nas VMs
vagrant status | Verifica se VM estão ativas ou não.
vagrant ssh 'vm'  | Acessa a VM
vagrant ssh 'vm' -c 'comando' | Executa comando via ssh
vagrant reload 'vm' | Reinicia a VM
vagrant halt  | Desliga as VMs

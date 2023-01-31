# Ansible

## O que é e pra que serve?

- Utilitário open source para orquestração e gerenciamento de configuração;

- É uma ferramenta de IaC (infraestrutura como código);

- Usado para automatização e padronização de configurações de hosts virtuais (bare metal e máquinas virtuais);

- Arquitetura simples e de fácil uso.

<br />

## Arquitetura

- Funciona com dois tipos de máquina:

  - Controle node -> Máquina onde será instalado e configurado o Ansible. A partir dessa máquina os comandos são executados remotamente;
  - Managed hosts -> Hosts que serão gerenciados e configurados pelo Ansible.

- **Host Inventory**: Arquivo com lista de hosts que serão gerenciados pelo Ansible, que contém os IPs dos hosts;

- A Comunicação com os Hosts acontece via SSH;

- Nenhum software precisa ser instalado no Managed Host;

- Alguns dos seus módulos:
  - Core modules -> Executam a grande maioria das atividades de administração do sistema operacional;
  - Custom modules -> Extendem a funcionalidade do Ansible com componentes personalizados escritos em Python;
  - Playbooks -> Arquivo YAML com sintaxe pré-definida para configurar módulos Ansible;
  - Plugins -> Extensão de funcionalidade (envio de mensagens, emails, etc...);
  - Host Inventory -> IPs dos hosts que são gerenciados pelo Ansible;
  - Ansible Galaxy -> Site que disponibiliza um conjunto de roles (tarefas) desenvolvidas pela comunidade.

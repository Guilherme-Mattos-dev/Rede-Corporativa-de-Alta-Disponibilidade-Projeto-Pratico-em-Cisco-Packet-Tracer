Projeto Prático — Rede Corporativa

Instituição: Alpha Saúde

Integrantes do grupo

Guilherme Mattos dos Santos — 0028155
Renato Campos Lopes — 0028017
João Marcos dos Santos Antunes — 0028201
Phillipe Santana Gonzaga — 0026802
Douglas Gabriel Barboza Freitas — 0027692
Leonardo Lisboa dos Santos — 0027815

Cenário da empresa

A rede foi desenvolvida para uma empresa fictícia com os setores de Gerência, Desenvolvimento e Comercial. Para atender às necessidades de segmentação de tráfego, segurança e disponibilidade, foi utilizada uma estrutura com dois Core Switches Layer 3, quatro switches de acesso e agregação de links por EtherChannel.

Endereçamento IP e VLANs

VLAN 10 — Gerência
Rede: 192.168.10.0/24
Gateway: 192.168.10.1
Switch conectado: SW-ACESSO-1

VLAN 20 — Desenvolvimento
Rede: 192.168.20.0/24
Gateway: 192.168.20.1
Switch conectado: SW-ACESSO-2

VLAN 30 — Comercial
Rede: 192.168.30.0/24
Gateway: 192.168.30.1
Switches conectados: SW-ACESSO-3 e SW-ACESSO-4

VLAN 40 — Servidores
Rede: 192.168.40.0/24
Gateway: 192.168.40.1
Conexão: CORE-1 diretamente

Estrutura de dispositivos

2 Core Switches Layer 3, sendo o CORE-1 ativo e o CORE-2 utilizado como redundância física.
4 switches Layer 2 de acesso.
2 servidores: SRV-DHCP-DNS e SRV-APP.
32 PCs, sendo 8 PCs por switch de acesso.

EtherChannel

SW-ACESSO-1: Fa0/23-24 para CORE-1 Fa0/1-2 — Channel-Group 1.
SW-ACESSO-2: Fa0/23-24 para CORE-1 Fa0/3-4 — Channel-Group 2.
SW-ACESSO-3: Fa0/23-24 para CORE-1 Fa0/5-6 — Channel-Group 3.
SW-ACESSO-4: Fa0/23-24 para CORE-1 Fa0/7-8 — Channel-Group 4.

Roteamento Inter-VLAN

O roteamento entre as VLANs é realizado no CORE-1 por meio das interfaces VLAN, utilizando os seguintes gateways:

VLAN 10 — 192.168.10.1
VLAN 20 — 192.168.20.1
VLAN 30 — 192.168.30.1
VLAN 40 — 192.168.40.1

DHCP

O CORE-1 utiliza DHCP Relay para encaminhar as solicitações das VLANs 10, 20 e 30 para o servidor DHCP no endereço 192.168.40.10.

Os pools configurados no servidor são:

VLAN 10 — gateway 192.168.10.1 — início 192.168.10.20 — máscara 255.255.255.0 — DNS 8.8.8.8
VLAN 20 — gateway 192.168.20.1 — início 192.168.20.20 — máscara 255.255.255.0 — DNS 8.8.8.8
VLAN 30 — gateway 192.168.30.1 — início 192.168.30.20 — máscara 255.255.255.0 — DNS 8.8.8.8
VLAN 40 — gateway 192.168.40.1 — início 192.168.40.20 — máscara 255.255.255.0 — DNS 8.8.8.8

Testes de validação

Para verificar a configuração da rede, podem ser utilizados os seguintes comandos:

show vlan brief

show etherchannel summary

show ip route

show ip interface brief

Para verificar o DHCP, em um PC deve ser acessado Desktop > IP Configuration e selecionada a opção DHCP.

Para testar a comunicação entre VLANs, pode ser utilizado:

ping 192.168.40.10

Também pode ser realizado um ping entre PCs conectados a switches de acesso diferentes, utilizando PCs da mesma VLAN.

Arquivos do repositório

README.md — documentação da rede.
comandos-cli.txt — comandos utilizados na configuração e validação.
trabalho de redes.pkt — arquivo do Cisco Packet Tracer.

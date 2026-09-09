# 🌐 Infraestrutura de Rede Corporativa com DMZ e Troubleshooting DNS

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco%20Packet%20Tracer-005691?style=for-the-badge&logo=cisco&logoColor=white)
![Network Security](https://img.shields.io/badge/Networking-Inter--VLAN%20Routing-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

Projetação, implementação e diagnóstico de falhas em uma infraestrutura de rede corporativa segmentada (LAN + DMZ) desenvolvida no **Cisco Packet Tracer**. O projeto foca em roteamento de Camada 3 (Inter-VLAN), segmentação de segurança e resolução de nomes (DNS Tipo A) para acesso a serviços web internos.

---

## 🛠️ Arquitetura e Topologia da Rede

A topologia foi desenhada em uma estrutura hierárquica contendo rede local de clientes, switch core de distribuição L3, switch de acesso e servidores dedicados na DMZ.

![Topologia do Projeto](images/topologia.png)

### Tabela de Endereçamento e Interfaces

| Dispositivo | Interface | Endereço IP | Máscara de Sub-rede | Gateway Padrão | Função |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PC-CORP-01** | FastEthernet0 | `10.10.20.100` | `255.255.255.0` | `10.10.20.1` | Estação de trabalho corporativa |
| **SW-CORE-01** | Vlan10 (SVI) | `10.10.20.1` | `255.255.255.0` | N/A | Gateway L3 da LAN Corporativa |
| **SW-CORE-01** | Vlan1 (SVI) | `192.168.100.1` | `255.255.255.0` | N/A | Gateway L3 da DMZ |
| **SRV-DNS-01** | FastEthernet0 | `192.168.100.20` | `255.255.255.0` | `192.168.100.1` | Servidor DNS Primário |
| **SRV-WEB-01** | FastEthernet0 | `192.168.100.10` | `255.255.255.0` | `192.168.100.1` | Servidor Web HTTP |

---

## ⚙️ Configurações Principais

### Roteamento Inter-VLAN no Switch Core (`SW-CORE-01`)
```text
SW-CORE-01> enable
SW-CORE-01# configure terminal
SW-CORE-01(config)# ip routing
SW-CORE-01(config)# interface Vlan1
SW-CORE-01(config-if)# ip address 192.168.100.1 255.255.255.0
SW-CORE-01(config-if)# no shutdown
SW-CORE-01(config-if)# exit
SW-CORE-01(config)# write memory

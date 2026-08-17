# introducao-as-redes-hierarquicas
# Atividade Prática: Introdução às Redes Hierárquicas
**Objetivo:** Compreender a divisão de uma rede corporativa nas três camadas do modelo hierárquico (Acesso, Distribuição e Núcleo/Core) e realizar a configuração e testes de conectividade básica.

Montei uma rede em 3 camadas, configurei os IPs e testei a comunicação.

---

### 1. Materiais

* **Núcleo (*Core*):** 1x Roteador Cisco 4331
* **Distribuição:** 1x Switch Cisco 3650
* **Acesso:** 2x Switches Cisco 2960 (`SW-Acesso-Lab` e `SW-Acesso-Sec`)
* **Dispositivos Finais:** 4x PCs (`PC-Lab01`, `PC-Lab02`, `PC-Sec01`, `PC-Sec02`)
* **Cabos:** Cabos Diretos (*Straight-Through*)

---

### 2. Conexões de Rede

| Dispositivo Origem | Porta Origem | Dispositivo Destino | Porta Destino |
| --- | --- | --- | --- |
| **PC-Lab01 / PC-Lab02** | Fa0 | SW-Acesso-Lab | Fa0/1 e Fa0/2 |
| **PC-Sec01 / PC-Sec02** | Fa0 | SW-Acesso-Sec | Fa0/1 e Fa0/2 |
| **SW-Acesso-Lab** | Gi0/1 | SW-Distribuição-3650 | Gi1/0/1 |
| **SW-Acesso-Sec** | Gi0/1 | SW-Distribuição-3650 | Gi1/0/2 |
| **SW-Distribuição-3650** | Gi1/0/24 | Roteador-Core-4331 | Gi0/0/0 |

---

### 3. Passo a Passo de Configuração

1. **Montagem Física:**
* Conectei a fonte de alimentação (*AC Power Supply*) no `SW-Distribuição-3650` (aba **Physical**).
* Fiz as conexões com cabos diretos conforme a tabela acima.


2. **Configuração dos PCs:**
* Em cada PC (**Desktop > IP Configuration**), configurei o IP na faixa `192.168.1.X`, a máscara `255.255.255.0` e o Gateway `192.168.1.1`.
* *Exemplo para PC-Sec02:* IP `192.168.1.20`.


3. **Configuração do Roteador:**
* No `Roteador-Core-4331` (aba **CLI**), executei:
```text
enable
configure terminal
interface gigabitEthernet 0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

```





---

### 4. Testes de Conectividade

1. **Terminal (PC-Lab01):**
* Executei `ping 192.168.1.20` (testa comunicação entre setores).
* Executei `ping 192.168.1.1` (testa alcance ao Roteador).


2. **Simulação:**
* Mudei para o modo **Simulation** e filtrei apenas o protocolo **ICMP**.
* Usei o envelope PDU do `PC-Lab01` até o `Roteador-Core-4331` para visualizar o pacote subindo a hierarquia: **Acesso $\rightarrow$ Distribuição $\rightarrow$ Núcleo**.



---


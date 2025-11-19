# UNIBRAS - Modelo de Documento para Projetos, Pesquisas e Disciplinas Específicas

<p align="center">
  <a href="https://sejaunibras.com.br"><img src="assets/unibras-logo.png" alt="UNIBRAS Logo" border="0" width="70%" /></a>
</p>

---

# Configuração e Análise dos Protocolos de Roteamento Dinâmico IPv6
## RIPng, EIGRPv6 e OSPFv3

> Trabalho Prático — Disciplina de Redes de Computadores

<p align="center">
  <img alt="Status" src="https://img.shields.io/badge/status-concluido-green">
  <img alt="Valor" src="https://img.shields.io/badge/valor-1.5%20pontos-blue">
  <img alt="Universidade" src="https://img.shields.io/badge/universidade-UNIBRAS-red">
</p>

---

## 👥 Informações do Projeto

### 📚 Disciplina
**Redes de Computadores**

### 👨‍🎓 Aluno(a)
- [CARLOS EDUARDO]()

### 👨‍🏫 Orientador(a)
- **Prof.** [FRANCISMAR ALVES MARTINS JUNIOR](https://www.linkedin.com/in/francismar-alves-martins-junior-8a320b90/)

---

## 🎯 Objetivo da Atividade

Configurar e analisar o funcionamento dos principais protocolos de roteamento dinâmico em redes IPv6 (RIPng, EIGRPv6 e OSPFv3), através de uma topologia composta por três roteadores interligados em série, utilizando simuladores de rede.

### 📋 Requisitos Obrigatórios

1. **Topologia:** 3 roteadores interligados em série (R1–R2–R3)
2. **Interfaces por Roteador:**
   - 1 interface Loopback (representando rede local)
   - 2 interfaces de enlace IPv6 (comunicação entre roteadores)
3. **Endereçamento:** IPv6 com prefixo 2001:DB8::/32
4. **Roteamento:** Comando `ipv6 unicast-routing` habilitado em todos os roteadores
5. **Protocolos:** Implementação completa de RIPng, EIGRPv6 e OSPFv3

### 📊 Critérios de Avaliação

| Item | Pontuação | Descrição |
|------|-----------|-----------|
| **RIPng Configurado** | 0,5 pt | Funcionamento correto do protocolo RIPng |
| **EIGRPv6 Configurado** | 0,5 pt | Funcionamento correto do protocolo EIGRPv6 |
| **OSPFv3 Configurado** | 0,5 pt | Funcionamento correto do protocolo OSPFv3 |
| **Organização e Documentação** | 0,3 pt | Estrutura do repositório GitHub e README.md |
| **Demonstração em Vídeo** | 0,2 pt | Clareza e completude do vídeo no YouTube |
| **Bônus: Teste de Falha e Reconvergência** | 0,2 pt | Teste opcional de falha de enlace |
| **TOTAL** | **1,5 pt** | **(até 1,7 pt com bônus)** |

---

## 🔬 1️⃣ Relatório Técnico — Redes de Computadores (IPv6)

### 📝 Resumo

Este trabalho prático implementa a configuração e análise comparativa dos três principais protocolos de roteamento dinâmico em redes IPv6:

- **RIPng** (Routing Information Protocol Next Generation)
- **EIGRPv6** (Enhanced Interior Gateway Routing Protocol for IPv6)
- **OSPFv3** (Open Shortest Path First version 3)

A topologia utilizada é composta por três roteadores Cisco (R1, R2 e R3) interligados em série, onde cada roteador possui uma interface loopback representando uma rede local e duas interfaces de enlace para comunicação entre roteadores. A atividade envolve a configuração de cada protocolo, verificação de vizinhanças, análise de tabelas de rotas e testes de conectividade completa entre todas as redes.

### 🎯 Palavras‑chave

IPv6; RIPng; EIGRPv6; OSPFv3; Roteamento; Redes Cisco; Topologia.

### 🕹️ Introdução

O crescimento exponencial de dispositivos conectados demanda protocolos de comunicação mais eficientes. O IPv6 foi criado para lidar com o esgotamento do IPv4 e traz mudanças significativas, incluindo novos formatos de endereços e protocolos de roteamento adaptados.

Este trabalho tem como foco principal a implementação, configuração e validação de três protocolos dinâmicos amplamente utilizados em ambientes corporativos:

RIPng — evolução do RIP para IPv6
EIGRPv6 — versão IPv6 do protocolo proprietário Cisco
OSPFv3 — adaptação do OSPF para IPv6

A proposta é comparar a operação de cada protocolo no mesmo cenário.

### ⚡️ Metodologia

#### 🔧 Ambiente Utilizado

| Componente | Descrição |
|-----------|-----------|
| **Simulador** | Cisco Packet Tracer |
| **Equipamentos** | 3 Roteadores Cisco série 2901 |
| **Protocolo de Rede** | IPv6 |
| **Endereçamento Base** | 2001:DB8::/32 |
| **Links** | Seriais ponto-a-ponto (/127) |
| **Redes Locais** | Loopbacks (/64) |
| **Cabos** | Serial DCE/DTE |

#### 🔌 Topologia da Rede

```
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│     R1      │ Serial  │     R2      │ Serial  │     R3      │
│  (Cisco)    │◄───────►│  (Cisco)    │◄───────►│  (Cisco)    │
└─────────────┘         └─────────────┘         └─────────────┘
      │                        │                        │
   Lo0: 2001:DB8:            Lo0: 2001:DB8:            Lo0: 2001:DB8:
   CAFE:1::1/64             CAFE:2::1/64             CAFE:3::1/64
```

#### 📍 Endereçamento IPv6

| Roteador | Loopback | Link para R2 | Link para R3 |
|----------|----------|--------------|--------------|
| **R1** | 2001:DB8:CAFE:1::1/64 | 2001:DB8:CAFE:F::1/127 | N/A |
| **R2** | 2001:DB8:CAFE:2::1/64 | 2001:DB8:CAFE:F::0/127 | 2001:DB8:CAFE:E::1/127 |
| **R3** | 2001:DB8:CAFE:3::1/64 | N/A | 2001:DB8:CAFE:E::0/127 |

## 📊 Resultados e Análise

### 🔹 RIPng (Routing Information Protocol Next Generation)

**Características:**
- Tipo: Protocolo de Vetor de Distância
- Métrica: Número de saltos (máximo 15)
- Convergência: Lenta (30 segundos entre atualizações)
- Escalabilidade: Baixa (inadequado para redes grandes)

**Configuração Mínima:**
```
ipv6 unicast-routing
interface Loopback0
 ipv6 address 2001:DB8:CAFE:X::1/64
 ipv6 rip RIPNG enable
interface Serial0/3/0
 ipv6 address 2001:DB8:CAFE:F::X/127
 ipv6 rip RIPNG enable
ipv6 router rip RIPNG
```

**Verificação:**
```
show ipv6 rip                    # Informações do protocolo
show ipv6 rip database           # Banco de dados com rotas
show ipv6 route rip              # Rotas aprendidas por RIPng
```

**Resultados Documentados em `prints-comandos/RIPng/`:**
- Interfaces IPv6 configuradas
- Banco de dados RIPng
- Tabela de rotas IPv6

---

### 🔹 EIGRPv6 (Enhanced Interior Gateway Routing Protocol for IPv6)

**Características:**
- Tipo: Protocolo Híbrido (vetor de distância + estado de enlace)
- Métrica: Composite (bandwidth, delay, reliability, load, MTU)
- Convergência: Rápida (suporta DUAL)
- Escalabilidade: Alta (adequado para redes médias/grandes)
- AS Number: 100

**Configuração Mínima:**
```
ipv6 unicast-routing
interface Loopback0
 ipv6 address 2001:DB8:CAFE:X::1/64
 ipv6 eigrp 100
interface Serial0/3/0
 ipv6 address 2001:DB8:CAFE:F::X/127
 ipv6 eigrp 100
ipv6 router eigrp 100
```

**Verificação:**
```
show ipv6 eigrp neighbors        # Vizinhos EIGRP
show ipv6 eigrp topology         # Topologia EIGRP
show ipv6 route eigrp            # Rotas aprendidas por EIGRPv6
```

**Resultados Documentados em `prints-comandos/EIGRPv6/`:**
- Interfaces IPv6 configuradas
- Vizinhos e topologia EIGRP
- Tabela de rotas IPv6

---

### 🔹 OSPFv3 (Open Shortest Path First version 3)

**Características:**
- Tipo: Protocolo de Estado de Enlace
- Métrica: Custo baseado em bandwidth
- Convergência: Rápida (SPF - Shortest Path First)
- Escalabilidade: Alta (melhor para redes grandes)
- Area ID: 0 (Backbone)
- Process ID: 10

**Configuração Mínima:**
```
ipv6 unicast-routing
interface Loopback0
 ipv6 address 2001:DB8:CAFE:X::1/64
 ipv6 ospf 10 area 0
interface Serial0/3/0
 ipv6 address 2001:DB8:CAFE:F::X/127
 ipv6 ospf 10 area 0
ipv6 router ospf 10
```

**Verificação:**
```
show ipv6 ospf neighbor          # Vizinhos OSPF
show ipv6 ospf                   # Informações gerais do OSPF
show ipv6 ospf database          # Banco de dados de enlaces (LSA)
show ipv6 route ospf             # Rotas aprendidas por OSPFv3
```

**Resultados Documentados em `prints-comandos/OSPFv3/`:**
- Interfaces IPv6 configuradas
- Vizinhos OSPF
- Informações OSPF e banco de dados
- Tabela de rotas IPv6

---

### 🎓 Aprendizados e Observações

1. **RIPng** é excelente para introdução a roteamento IPv6, mas sua limitação de 15 saltos o torna impraticável para redes maiores.

2. **EIGRPv6** oferece um bom balanço entre funcionalidade e complexidade, com convergência rápida e suporte a métricas sofisticadas, sendo ideal para redes corporativas de médio porte.

3. **OSPFv3** é o padrão da indústria para roteamento dinâmico em redes IPv6 grandes e complexas, com excelente escalabilidade e suporte a múltiplas áreas.

4. Todos os três protocolos funcionam corretamente em IPv6 e garantem redundância e confiabilidade quando corretamente configurados.

### 🚀 Como Usar Este Projeto

#### 📥 Pré-requisitos
- Cisco Packet Tracer, GNS3 ou EVE-NG instalado
- Acesso aos arquivos de topologia em `topologias/`
- Conhecimento básico de roteamento e IPv6

#### 📖 Passos para Reproduzir

1. **Abra o simulador** e carregue a topologia desejada:
   ```
   topologias/RIPng.pkt
   topologias/EIGRPv6.pkt
   topologias/OSPFv3.pkt
   ```

2. **Verifique o endereçamento** executando em cada roteador:
   ```
   Router#show ipv6 interface brief
   ```

3. **Configure o protocolo desejado** usando os arquivos em `configurações/` como referência

4. **Verifique a vizinhança:**
   - **RIPng:** `show ipv6 rip`
   - **EIGRPv6:** `show ipv6 eigrp neighbors`
   - **OSPFv3:** `show ipv6 ospf neighbor`

5. **Analise as rotas aprendidas:**
   ```
   Router#show ipv6 route
   ```

6. **Teste a conectividade:**
   ```
   Router#ping 2001:DB8:CAFE:X::1
   Router#traceroute 2001:DB8:CAFE:X::1
   ```

### 💡 Comandos de Diagnóstico e Verificação

#### Comandos Comuns (Todos os Protocolos)

```bash
# Verificar interfaces IPv6
show ipv6 interface brief

# Visualizar tabela de rotas IPv6
show ipv6 route

# Ver tabela de vizinhança IPv6
show ipv6 neighbors

# Teste de conectividade
ping 2001:DB8:CAFE:X::1
traceroute 2001:DB8:CAFE:X::1
```

#### Comandos Específicos RIPng

```bash
# Informações gerais do RIPng
show ipv6 rip

# Banco de dados RIPng com rotas aprendidas
show ipv6 rip database

# Rotas aprendidas por RIPng
show ipv6 route rip
```

#### Comandos Específicos EIGRPv6

```bash
# Vizinhos EIGRP
show ipv6 eigrp neighbors

# Topologia EIGRP (Topology Table)
show ipv6 eigrp topology

# Rotas aprendidas por EIGRPv6
show ipv6 route eigrp
```

#### Comandos Específicos OSPFv3

```bash
# Informações gerais do OSPF
show ipv6 ospf

# Vizinhos OSPF
show ipv6 ospf neighbor

# Banco de dados de enlaces (LSA)
show ipv6 ospf database

# Rotas aprendidas por OSPFv3
show ipv6 route ospf
```

---

## 📂 Estrutura do Repositório

```
Trabalho-Redes/
├── README.md                           # Este arquivo
├── assets/
│   ├── unibras-logo.png
├── configurações/                            # Arquivos de configuração (show running-conf)
│   ├── RIPng/
│   │   ├── R1-ripng.txt               # show running-conf do R1
│   │   ├── R2-ripng.txt               # show running-conf do R2
│   │   └── R3-ripng.txt               # show running-conf do R3
│   ├── EIGRPv6/
│   │   ├── R1-eigrp.txt               # show running-conf do R1
│   │   ├── R2-eigrp.txt               # show running-conf do R2
│   │   └── R3-eigrp.txt               # show running-conf do R3
│   └── OSPFv3/
│       ├── R1-ospf.txt                # show running-conf do R1
│       ├── R2-ospf.txt                # show running-conf do R2
│       └── R3-ospf.txt                # show running-conf do R3
│
├── topologias/                         # Arquivos Cisco Packet Tracer (.pkt)
│   ├── RIPng.pkt                      # Topologia com RIPng
│   ├── EIGRPv6.pkt                    # Topologia com EIGRPv6
│   ├── OSPFv3.pkt                     # Topologia com OSPFv3
│   └── BASE.pkt               # Topologia base (sem configuração)
│
├── prints-comandos/                             # Documentação visual (capturas de tela)
│   ├── RIPng/
│   │   ├── RIPngR1- show ipv6 interface brief.png
│   │   ├── RIPngR1- show ipv6 rip database.png
│   │   ├── RIPngR1- show ipv6 route.png
│   │   ├── RIPngR2- show ipv6 interface brief.png
│   │   ├── RIPngR2- show ipv6 rip database.png
│   │   ├── RIPngR2- show ipv6 route.png
│   │   ├── RIPngR3- show ipv6 interface brief.png
│   │   ├── RIPngR3- show ipv6 rip database.png
│   │   └── RIPngR3- show ipv6 route.png
│   │
│   ├── EIGRPv6/
│   │   ├── EIGRPv6R1- show ipv6 interface brief.png
│   │   ├── EIGRPv6R1- show ipv6 eigrp neighbors e show ipv6 eigrp topology.png
│   │   ├── EIGRPv6R1- show ipv6 route.png
│   │   ├── EIGRPv6R2- show ipv6 interface brief.png
│   │   ├── EIGRPv6R2- show ipv6 eigrp neighbors e show ipv6 eigrp topology.png
│   │   ├── EIGRPv6R2- show ipv6 route.png
│   │   ├── EIGRPv6R3- show ipv6 interface brief.png
│   │   ├── EIGRPv6R3- show ipv6 eigrp neighbors e show ipv6 eigrp topology.png
│   │   └── EIGRPv6R3- show ipv6 route.png
│   │
│   └── OSPFv3/
│       ├── OSPFv3R1- show ipv6 interface brief.png
│       ├── OSPFv3R1- show ipv6 ospf neighbor.png
│       ├── OSPFv3R1- show ipv6 ospf.png
│       ├── OSPFv3R1- show ipv6 route.png
│       ├── OSPFv3R2- show ipv6 interface brief.png
│       ├── OSPFv3R2- show ipv6 ospf neighbor.png
│       ├── OSPFv3R2- show ipv6 ospf.png
│       ├── OSPFv3R2- show ipv6 route.png
│       ├── OSPFv3R3- show ipv6 interface brief.png
│       ├── OSPFv3R3- show ipv6 ospf neighbor.png
│       ├── OSPFv3R3- show ipv6 ospf.png
│       └── OSPFv3R3- show ipv6 route.png
```

---

## ✅ Checklist de Entrega

- [x] Topologia com 3 roteadores interligados em série
- [x] Interfaces loopback configuradas (2001:DB8:CAFE:X::1/64)
- [x] Roteamento IPv6 habilitado (`ipv6 unicast-routing`)
- [x] RIPng configurado e testado
- [x] EIGRPv6 configurado e testado
- [x] OSPFv3 configurado e testado
- [x] Conectividade completa entre as loopbacks validada
- [x] Arquivos de configuração documentados em `configurações/`
- [x] Capturas de tela dos comandos em `prints-comandos/`
- [x] Topologias em `topologias/`
- [x] README.md completo e bem estruturado
- [x] Repositório GitHub com link na descrição do vídeo
- [ ] Vídeo demonstrativo no YouTube (4-6 minutos)
- [ ] *Opcional:* Teste de falha e reconvergência

---

## ⚡️ Ambiente e Ferramentas Utilizadas

* **Simulador:** Cisco Packet Tracer
* **Equipamentos:** Roteadores Cisco série 2901
* **Protocolo de Rede:** IPv6 (Internet Protocol version 6)
* **Padrão de Endereçamento:** 2001:DB8::/32 (documentação)
* **Sistema Operacional:** Cisco IOS 15.1
* **Controle de Versão:** Git e GitHub

### 📈 Testes Realizados

**Para cada protocolo foram executados:**

1. ✅ **Verificação de Interfaces:** `show ipv6 interface brief`
2. ✅ **Teste de Vizinhança:** Validação da formação de adjacências
3. ✅ **Análise de Rotas:** `show ipv6 route`
4. ✅ **Banco de Dados do Protocolo:** Informações específicas de cada protocolo
5. ✅ **Teste de Ping:** Conectividade entre loopbacks
6. ✅ **Teste de Traceroute:** Rastreamento de caminho entre roteadores

### 🎓 Conclusões

Este trabalho prático demonstrou com sucesso a implementação e funcionamento dos três principais protocolos de roteamento dinâmico em IPv6:

- **RIPng:** Protocolo simples, ideal para aprendizado inicial, mas com limitações claras para ambientes maiores
- **EIGRPv6:** Excelente balanceamento entre funcionalidade e complexidade, convergência rápida via DUAL
- **OSPFv3:** Padrão da indústria, máxima escalabilidade e funcionalidades avançadas

A implementação bem-sucedida valida o conhecimento em protocolos de roteamento dinâmico IPv6 e capacita para ambientes de produção.

---

## 📋 Licença e Informações Importantes

**Este trabalho foi desenvolvido como parte da disciplina de Redes de Computadores da UNIBRAS.**

- Aluno: [CARLOS EDUARDO]()
- Orientador: Prof. [FRANCISMAR ALVES MARTINS JUNIOR](https://www.linkedin.com/in/francismar-alves-martins-junior-8a320b90/)
- Instituição: Centro Universitário Montes Belos - UNIBRAS
- Data de Conclusão: 19 de novembro de 2025

**Aviso Legal:** 
- Cisco Packet Tracer é de propriedade da Cisco Systems, Inc.
- Este projeto é para fins educacionais apenas
- Todos os comandos foram testados em Cisco Packet Tracer

---

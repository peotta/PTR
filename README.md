# ENE0025 - Protocolos de Transporte e Roteamento (PTR)

- **Curso:** Engenharia de Redes de Comunicação  
- **Instituição:** Universidade de Brasília (UnB)  
- **Departamento:** Departamento de Engenharia Elétrica (ENE)  
- **Professor Responsável:** Prof. Dr. Laerte Peotta de Melo  

---

## Equipe de Monitoria

### Monitores Atuais (2026/02)

- Ana Cecília Braga
- Caio Lucas Pereira Mena Barreto
- Caio Soares Rodrigues
- Luidi Rafael da Silva Fernandes

### Monitores Anteriores (2026/01)

- Beatriz Silva Nascimento
- Gabriel Henrique da Cruz Costa
- Luan Silva Moura
- Luidi Rafael da Silva Fernandes

---

## Apresentação

A disciplina **Protocolos de Transporte e Roteamento** tem como objetivo apresentar os fundamentos, o funcionamento interno e a aplicação prática dos principais protocolos que sustentam a comunicação em redes IP modernas.

O curso aborda tanto os **protocolos da camada de transporte** quanto os **protocolos de roteamento**, enfatizando os mecanismos que permitem confiabilidade, escalabilidade, convergência, resiliência e desempenho na Internet.

Além da fundamentação teórica, a disciplina possui forte **componente prático**, com atividades de laboratório desenvolvidas em ambiente de emulação de redes utilizando o **PNetLab**, permitindo que os estudantes observem o comportamento real dos protocolos estudados.

---

<h2>Podcast da disciplina</h2>

<table>
  <tr>
    <td width="320" align="center">
      <a href="https://spotifycreators-web.app.link/e/4Wu544oVN1b">
        <img src="images/latencia-zero-podcast.png" alt="Latência Zero - Engenharia de Redes da UnB" width="280">
      </a>
    </td>
    <td valign="top">
      <p>
        O podcast <strong>Latência Zero</strong> apresenta discussões relacionadas a temas
        abordados em aula, com ênfase em <strong>redes de computadores</strong>,
        <strong>latência</strong>, <strong>infraestrutura de comunicação</strong> e
        aspectos práticos da engenharia de redes.
      </p>
      <p>
        <a href="https://spotifycreators-web.app.link/e/4Wu544oVN1b">Ouvir no Spotify</a>
      </p>
    </td>
  </tr>
</table>

---



## Objetivos da Disciplina

Ao final da disciplina, o estudante deverá ser capaz de:

- Compreender o funcionamento dos protocolos TCP e UDP
- Analisar mecanismos de controle de fluxo e congestionamento
- Entender o processo de encaminhamento IP e decisão de rotas
- Configurar e avaliar roteamento estático e dinâmico
- Implementar e comparar protocolos de roteamento intra-domínio (RIP e OSPF)
- Projetar e analisar cenários de roteamento interdomínio com BGP
- Aplicar políticas de roteamento e princípios de engenharia de tráfego
- Diagnosticar falhas e problemas de desempenho em redes IP

---

## Conteúdos Abordados

- Arquitetura TCP/IP
- Encaminhamento IP e tabelas de rotas
- Roteamento estático
- Roteamento dinâmico
- RIP: funcionamento e limitações
- OSPF: estado de enlace, métricas e áreas
- BGP: sistemas autônomos, atributos e políticas
- Integração entre IGP e BGP
- Convergência, escalabilidade e resiliência
- Aspectos de segurança em protocolos de roteamento

---
## Metodologia

As atividades laboratoriais serão desenvolvidas de forma **prática e supervisionada**, envolvendo:
- Configuração direta de equipamentos;
- Análise de saídas de comandos;
- Observação do comportamento da rede;
- Registro técnico das atividades realizadas.

O aluno deve seguir rigorosamente os roteiros e registrar os resultados conforme solicitado.

--- 

## Atividades Práticas

As atividades práticas são realizadas no **PNetLab** e incluem:

- Montagem de topologias IP
- Configuração de endereçamento e gateways
- Análise de tabelas de roteamento
- Implementação de RIP, OSPF e BGP
- Simulação de falhas de enlace
- Avaliação de convergência e políticas de roteamento
- Projeto final integrador de rede

Cada laboratório está diretamente vinculado ao conteúdo teórico apresentado em aula.

---
## Avaliação

A avaliação da disciplina será baseada em:
- Execução correta dos laboratórios;
- Qualidade dos registros e respostas apresentadas;
- Participação e envolvimento durante as atividades;
- Cumprimento dos prazos estabelecidos.

Os critérios específicos de cada experimento serão informados no respectivo roteiro.

---

## Requisitos

- Conhecimentos básicos de redes de computadores;
- Familiaridade com sistemas operacionais;
- Noções iniciais de protocolos TCP/IP;
- Atenção às normas de uso do laboratório.
---

## Bibliografia Básica

- **DOYLE, Jeff; CARROLL, Jennifer DeHaven**. Routing TCP/IP: volume 1. Indianapolis: Cisco Press, 1998.
- **FOROUZAN, Behrouz A.** Protocolo TCP/IP. 3. ed. Porto Alegre: AMGH, 2010.

## Bibliografia Complementar

- **KUROSE, James F.; ROSS, Keith W**. Redes de computadores e a Internet: uma abordagem top-down. 6. ed. São Paulo: Pearson, 2013.
- **TANENBAUM, Andrew S.; WETHERALL, David J.** Redes de computadores. 5. ed. São Paulo: Pearson, 2011.
- **STALLINGS, William.** Comunicações de dados e redes de computadores. 10. ed. São Paulo: Pearson, 2014.
- **COMER, Douglas E.** Interligação de redes com TCP/IP: princípios, protocolos e arquitetura. 5. ed. Rio de Janeiro: Elsevier, 2006.

## Documentos Normativos e Técnicos
- **POSTEL, Jon.** Transmission Control Protocol. RFC 793. Marina del Rey: ISI, 1981.
- **POSTEL, Jon.** User Datagram Protocol. RFC 768. Marina del Rey: ISI, 1980.
- **MOY, John T.** OSPF version 2. RFC 2328. Marina del Rey: ISI, 1998.
- **REKHTER, Yakov et al.** A border gateway protocol 4 (BGP-4). RFC 4271. Marina del Rey: ISI, 2006.

---

## Como usar este repositório
1. Abra a lista de laboratórios abaixo.
2. Em cada laboratório, siga as instruções e entregue conforme orientação do professor.

## Laboratórios

Os laboratórios práticos estão organizados de acordo com a progressão temática do curso:

### Módulo 0: Fundamentos e Ambiente PNetLab
| Laboratório | Tema | Roteiro |
|:------------:|------|:-------:|
| **00** | Guia de Comandos Básicos (VPCS e Linux) | [Acessar](./labs/comandos.md) |
| **01** | Configuração Inicial e Fundamentos de Roteamento IP | [Acessar](./labs/lab01.md) |
| **02** | Configuração Básica de Roteadores no PNetLab | [Acessar](./labs/lab02.md) |

### Módulo 1: Roteamento Intra-Domínio (IGP) e Multicast
| Laboratório | Tema | Roteiro |
|:------------:|------|:-------:|
| **03** | Roteamento Multicast: PIM-DM em Topologia Controlada | [Acessar](./labs/lab03.md) |
| **04** | Roteamento com RIPv2 e Análise de Convergência | [Acessar](./labs/lab04.md) |
| **05** | Roteamento Dinâmico com OSPF | [Acessar](./labs/lab05.md) |

### Módulo 2: Roteamento Inter-Domínio (EGP / BGP)
| Laboratório | Tema | Roteiro |
|:------------:|------|:-------:|
| **06** | Roteamento Externo via BGP (eBGP Básico) | [Acessar](./labs/lab06.md) |
| **07** | Configuração dos Provedores (BGP Externo e Peering) | [Acessar](./labs/lab07.md) |
| **08** | Políticas de Roteamento BGP e Integração com OSPF | [Acessar](./labs/lab08.md) |

### Módulo 3: Comutação por Rótulos (MPLS)
| Laboratório | Tema | Roteiro |
|:------------:|------|:-------:|
| **09** | Implementação de MPLS e LDP no Backbone | [Acessar](./labs/lab09.md) |

### Módulo 4: Serviços de Rede e Infraestrutura
| Laboratório | Tema | Roteiro |
|:------------:|------|:-------:|
| **13** | Configuração e Análise do Protocolo DHCP | [Acessar](./labs/lab13.md) |
| **13B** | Segurança em DHCP: Rogue Server, Análise e Mitigação (DHCP Snooping) | [Acessar](./labs/lab13B.md) |

### Módulo 5: Segurança de Redes e Aplicação
| Laboratório | Tema | Roteiro |
|:------------:|------|:-------:|
| **10** | Firewall de Pacotes Stateless com `iptables` | [Acessar](./labs/lab10.md) |
| **10B** | Firewall Stateful com `iptables` e Conntrack | [Acessar](./labs/lab10B.md) |
| **11A** | Implementação de WAF com ModSecurity e OWASP CRS | [Acessar](./labs/lab11A.md) |
| **11B** | Testes de Ataques Web e Análise de Logs no WAF | [Acessar](./labs/lab11B.md) |
| **12** | Implementação de IDS/IPS com Suricata no PNetLab | [Acessar](./labs/lab12.md) |

---

## Guias e Materiais Complementares

| Documento | Descrição | Link |
|-----------|-----------|:----:|
| **Comandos de Rede** | Tabela rápida de comandos para VPCS e distribuições Debian/Ubuntu | [Acessar](./labs/comandos.md) |
| **Ambiente Móvel & Auditoria** | Guia de instalação LineageOS + Magisk + Kali NetHunter (Xiaomi Pyxis) | [Acessar](./labs/linux-mobile.md) |

---

> Este repositório é de uso acadêmico e destina-se exclusivamente às atividades da disciplina.




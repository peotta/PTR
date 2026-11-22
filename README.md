# ENE0025 - Protocolos de Transporte e Roteamento (PTR)

- **Instituição:** Universidade de Brasília (UnB)
- **Departamento:** Departamento de Engenharia Elétrica (ENE)
- **Curso:** Engenharia de Redes de Comunicação
- **Disciplina:** ENE0025 - Protocolos de Transporte e Roteamento
- **Professor responsável:** Prof. Dr. Laerte Peotta de Melo

---

## 1. Equipe de Monitoria

| Monitores Atuais (2026/02) | Monitores Anteriores (2026/01) |
|----------------------------|--------------------------------|
| Ana Cecília Braga | Beatriz Silva Nascimento |
| Caio Lucas Pereira Mena Barreto | Gabriel Henrique da Cruz Costa |
| Caio Soares Rodrigues | Luan Silva Moura |
| Luidi Rafael da Silva Fernandes | Luidi Rafael da Silva Fernandes |

---

## 2. Apresentação

A disciplina **Protocolos de Transporte e Roteamento** tem como objetivo apresentar os fundamentos, o funcionamento interno e a aplicação prática dos principais protocolos que sustentam a comunicação em redes IP modernas.

O curso aborda tanto os **protocolos da camada de transporte** quanto os **protocolos de roteamento**, além das **principais aplicações de rede**, enfatizando os mecanismos que permitem confiabilidade, escalabilidade, convergência, resiliência, segurança e desempenho na Internet.

Além da fundamentação teórica, a disciplina possui forte **componente prático**, com atividades de laboratório desenvolvidas em ambiente de emulação de redes utilizando o **PNetLab**, permitindo que os estudantes observem o comportamento real dos protocolos e serviços estudados.

---

### Material de Apoio: Podcast Latência Zero

<table>
  <tr>
    <td width="140" align="center">
      <a href="https://spotifycreators-web.app.link/e/4Wu544oVN1b">
        <img src="images/latencia-zero-podcast.png" alt="Latência Zero - Engenharia de Redes da UnB" width="120">
      </a>
    </td>
    <td valign="top">
      O podcast <strong>Latência Zero</strong> apresenta discussões técnicas complementares sobre os temas abordados em aula, com ênfase em redes de computadores, latência, infraestrutura de comunicação e aspectos práticos da engenharia de redes.<br><br>
      🎧 <a href="https://spotifycreators-web.app.link/e/4Wu544oVN1b">Ouvir no Spotify</a>
    </td>
  </tr>
</table>

### Material de Apoio: Simul-Net

<table>
  <tr>
    <td width="140" align="center">
      <a href="https://peotta.github.io/Simul-Net/">
        <img src="images/simul-net-logo.png" alt="Simul-Net - Simuladores de redes e protocolos" width="120">
      </a>
    </td>
    <td valign="top">
      O <strong>Simul-Net</strong> reúne simuladores visuais, executados no navegador, que mostram passo a passo o funcionamento dos protocolos estudados na disciplina, com diagrama de sequência ou topologia, captura de pacotes e explicação do experimento. É um recurso complementar aos laboratórios do PNetLab e não exige instalação.<br><br>
      🌐 <a href="https://peotta.github.io/Simul-Net/">Acessar o Simul-Net</a>
    </td>
  </tr>
</table>

---

## 3. Objetivos da Disciplina

Ao final da disciplina, o estudante deverá ser capaz de:

- Compreender o funcionamento dos protocolos TCP e UDP;
- Analisar o funcionamento e os requisitos das principais aplicações de rede;
- Analisar mecanismos de controle de fluxo e congestionamento;
- Entender o processo de encaminhamento IP e decisão de rotas;
- Configurar e avaliar roteamento estático e dinâmico;
- Implementar e comparar protocolos de roteamento intra-domínio (RIP e OSPF);
- Projetar e analisar cenários de roteamento interdomínio com BGP;
- Aplicar políticas de roteamento e princípios de engenharia de tráfego;
- Compreender o roteamento multicast (PIM-DM) e a comutação por rótulos (MPLS e LDP);
- Configurar e avaliar mecanismos de segurança de rede e de aplicação (firewall *stateless* e *stateful*, *Web Application Firewall* - WAF e sistemas de detecção e prevenção de intrusões - IDS/IPS);
- Diagnosticar falhas e problemas de desempenho em redes IP.

---

## 4. Conteúdos Abordados

- Arquitetura TCP/IP
- Principais aplicações de rede e modelos de comunicação
- Encaminhamento IP e tabelas de rotas
- Roteamento estático
- Roteamento dinâmico
- RIP: funcionamento e limitações
- OSPF: estado de enlace e métricas (área única)
- BGP: sistemas autônomos, atributos e políticas
- Integração entre IGP e BGP
- Roteamento multicast (PIM-DM)
- Comutação por rótulos (MPLS e LDP)
- Convergência, escalabilidade e resiliência
- Aspectos de segurança em protocolos de roteamento
- Segurança de redes: firewall *stateless* e *stateful* (`iptables`), WAF (ModSecurity e OWASP CRS) e IDS/IPS (Suricata)
- Acesso remoto seguro (SSH) e análise de tráfego (Wireshark e tcpdump)

---

## 5. Metodologia

As atividades laboratoriais serão desenvolvidas de forma **prática e supervisionada**, envolvendo:
- Configuração direta de equipamentos;
- Análise de saídas de comandos;
- Observação do comportamento da rede;
- Registro técnico das atividades realizadas.

O aluno deve seguir rigorosamente os roteiros e registrar os resultados conforme solicitado.

---

## 6. Atividades Práticas

As atividades práticas são realizadas no **PNetLab** e incluem:

- Montagem de topologias IP;
- Configuração de endereçamento e gateways;
- Análise de tabelas de roteamento;
- Implementação de RIP, OSPF, BGP, multicast (PIM-DM) e MPLS;
- Simulação de falhas de enlace;
- Avaliação de convergência e políticas de roteamento;
- Configuração de firewall, WAF e IDS/IPS;
- Acesso remoto seguro (SSH) e captura de tráfego com Wireshark e tcpdump.

Cada laboratório está diretamente vinculado ao conteúdo teórico apresentado em aula.

---

## 7. Avaliação

A avaliação da disciplina será baseada em:
- Execução correta dos laboratórios;
- Qualidade dos registros e respostas apresentadas;
- Participação e envolvimento durante as atividades;
- Cumprimento dos prazos estabelecidos.

Os critérios específicos de cada experimento serão informados no respectivo roteiro.

---

## 8. Requisitos

- Conhecimentos básicos de redes de computadores;
- Familiaridade com sistemas operacionais;
- Noções iniciais de protocolos TCP/IP;
- Atenção às normas de uso do laboratório.

---

## 9. Laboratórios Práticos

Os laboratórios práticos estão organizados de acordo com a progressão temática do curso:

### 9.1 Módulo 0: Fundamentos e Ambiente PNetLab

| Laboratório | Tema | Roteiro | Podcast |
|:------------:|------|:-------:|:-------:|
| **00** | Guia de Comandos Básicos (VPCS e Linux) | [Acessar](https://peotta.github.io/PTR/labs/#/ref/comandos) | - |
| **01** | Fundamentos de Roteamento IP e Encaminhamento de Pacotes | [Acessar](https://peotta.github.io/PTR/labs/#/lab/01) | - |
| **02** | Configuração Básica de Roteadores no PNetLab | [Acessar](https://peotta.github.io/PTR/labs/#/lab/02) | - |

### 9.2 Módulo 1: Roteamento Intra-Domínio (IGP) e Multicast

| Laboratório | Tema | Roteiro | Podcast |
|:------------:|------|:-------:|:-------:|
| **03** | Roteamento Multicast: PIM-DM em Topologia Controlada | [Acessar](https://peotta.github.io/PTR/labs/#/lab/03) | [🎧 Ep. 1](https://open.spotify.com/episode/6autgkF6lifJAD8M3Xr0XR) |
| **04** | Roteamento com RIPv2 e Análise de Convergência | [Acessar](https://peotta.github.io/PTR/labs/#/lab/04) | [🎧 Ep. 2](https://open.spotify.com/episode/5My3JBmZoVyoKaOL1MGArI) |
| **05** | Roteamento Dinâmico com OSPF | [Acessar](https://peotta.github.io/PTR/labs/#/lab/05) | [🎧 Ep. 4](https://open.spotify.com/episode/6ha3fZPjrfBp8ZQNyIfTps?si=754a105ed6474063) |

### 9.3 Módulo 2: Roteamento Inter-Domínio (EGP / BGP)

| Laboratório | Tema | Roteiro | Podcast |
|:------------:|------|:-------:|:-------:|
| **06** | Roteamento Externo via BGP (eBGP Básico) | [Acessar](https://peotta.github.io/PTR/labs/#/lab/06) | [🎧 Ep. 5](https://open.spotify.com/episode/5h5COkh8c51req9tUxZhzs?si=20722c87de1b41aa) |
| **07** | Configuração dos Provedores (BGP Externo e Peering) | [Acessar](https://peotta.github.io/PTR/labs/#/lab/07) | - |
| **08** | Políticas de Roteamento BGP e Integração com OSPF | [Acessar](https://peotta.github.io/PTR/labs/#/lab/08) | - |

### 9.4 Módulo 3: Comutação por Rótulos (MPLS)

| Laboratório | Tema | Roteiro | Podcast |
|:------------:|------|:-------:|:-------:|
| **09** | Implementação de MPLS e LDP no Backbone | [Acessar](https://peotta.github.io/PTR/labs/#/lab/09) | [🎧 Ep. 6](https://open.spotify.com/episode/5RXovxuVQ6eLXa5pt2dUeR?si=dZE1TCGAQwyFAuxqumNnyQ) |

### 9.5 Módulo 4: Segurança de Redes e Aplicação

| Laboratório | Tema | Roteiro | Podcast |
|:------------:|------|:-------:|:-------:|
| **10** | Firewall de pacotes sem estado (stateless) | [Acessar](https://peotta.github.io/PTR/labs/#/lab/10) | [🎧 Ep. 7](https://open.spotify.com/episode/6mSMblRBIjOvmX0AgsO1ln?si=ccYN8DnmSEuR6XSJgDvBAA) |
| **11** | Firewall Stateful com `iptables` e Conntrack | [Acessar](https://peotta.github.io/PTR/labs/#/lab/11) | - |
| **12** | Implementação de WAF com ModSecurity e OWASP CRS | [Acessar](https://peotta.github.io/PTR/labs/#/lab/12) | - |
| **13** | Testes de Ataques Web e Análise de Logs no WAF | [Acessar](https://peotta.github.io/PTR/labs/#/lab/13) | - |
| **14** | Implementação de IDS/IPS com Suricata no PNetLab | [Acessar](https://peotta.github.io/PTR/labs/#/lab/14) | - |

---

## 10. Guias e Materiais Complementares

| Documento | Descrição | Link |
|-----------|-----------|:----:|
| **Comandos de Rede** | Tabela rápida de comandos para VPCS e distribuições Debian/Ubuntu | [Acessar](https://peotta.github.io/PTR/labs/#/ref/comandos) |

---

## 11. Bibliografia e Documentos Normativos

### 11.1 Bibliografia Básica

- **DOYLE, Jeff; CARROLL, Jennifer DeHaven**. Routing TCP/IP: volume 1. Indianapolis: Cisco Press, 1998.
- **FOROUZAN, Behrouz A.** Protocolo TCP/IP. 3. ed. Porto Alegre: AMGH, 2010.

### 11.2 Bibliografia Complementar

- **BRITO, Samuel Henrique Bucke**. Laboratórios de tecnologias Cisco em infraestrutura de redes. 2. ed. São Paulo: Novatec, 2014.
- **COMER, Douglas E.** Interligação de redes com TCP/IP: princípios, protocolos e arquitetura. 5. ed. Rio de Janeiro: Elsevier, 2006.
- **HALABI, Sam; MCPHERSON, Danny**. Internet routing architectures. 2. ed. Indianapolis: Cisco Press, 2001.
- **KUROSE, James F.; ROSS, Keith W**. Redes de computadores e a Internet: uma abordagem top-down. 8. ed. Porto Alegre: Pearson/Bookman, 2021.
- **LOBATO, Luiz Carlos**. Protocolos de roteamento IP. Rio de Janeiro: RNP/ESR, 2013.
- **MORAES, Alexandre Fernandes de**. Wireshark: guia prático de análise de tráfego de rede. São Paulo: Novatec, 2015.
- **STALLINGS, William.** Comunicações de dados e redes de computadores. 10. ed. São Paulo: Pearson, 2014.
- **TANENBAUM, Andrew S.; WETHERALL, David J.** Redes de computadores. 5. ed. São Paulo: Pearson, 2011.
- **ZWICKY, Elizabeth D.; COOPER, Simon; CHAPMAN, D. Brent**. Building internet firewalls. 2. ed. Sebastopol: O'Reilly, 2000.

### 11.3 Documentos Normativos e Técnicos

- **EDDY, Wesley (ed.).** Transmission Control Protocol (TCP). RFC 9293. [S.l.]: IETF, 2022. (Substitui a RFC 793.)
- **POSTEL, Jon.** User Datagram Protocol. RFC 768. Marina del Rey: ISI, 1980.
- **MOY, John T.** OSPF version 2. RFC 2328. Marina del Rey: ISI, 1998.
- **REKHTER, Yakov et al.** A border gateway protocol 4 (BGP-4). RFC 4271. Marina del Rey: ISI, 2006.

---

## 12. Uso de Inteligência Artificial

Em conformidade com a Política de Integridade Acadêmica e Uso Responsável da Inteligência Artificial da Faculdade de Tecnologia (FT/UnB), aprovada pelo Conselho da FT em 30/09/2026, estabelecem-se as seguintes diretrizes:

### 12.1 Declaração Docente
Declara-se que este material didático foi elaborado com apoio de ferramentas de inteligência artificial generativa (Claude, ChatGPT e Gemini), sob estrita supervisão, revisão técnica e responsabilidade do professor responsável.

### 12.2 Diretrizes para os Estudantes
- **Regime Geral da Disciplina:** O uso de ferramentas de IA generativa é **permitido** como instrumento de apoio ao aprendizado em todas as atividades laboratoriais (pesquisa conceitual de RFCs, esclarecimento de sintaxe de comandos, interpretação de saídas e suporte à redação técnica dos relatórios).
- **Responsabilidade Acadêmica:** O estudante é o único responsável pela exatidão técnica, autoria e originalidade de suas entregas. Todas as configurações práticas, comandos executados e capturas de telas e comandos devem ser obrigatoriamente produzidos pelo estudante.
- **Condutas Vedadas:**
  - Fabricar, adulterar ou simular saídas de comandos, capturas de telas e comandos ou evidências de laboratório;
  - Apresentar análises e conclusões elaboradas com o uso de IA sem reflexão, revisão ou contribuição intelectual própria;
  - Inserir dados sensíveis, credenciais de acesso ou informações confidenciais em plataformas públicas de IA.

# Laboratório 04 - RIP e análise de convergência

**Disciplina:** ENE0025 - Protocolos de Transporte e Roteamento  
**Professor responsável:** Prof. Dr. Laerte Peotta de Melo  

---

## 1. Tema

Implementação do **RIPv2** em topologia com múltiplos roteadores, seguida de **análise de convergência após falha de enlace**.

---

## 2. Justificativa

Este laboratório eleva o nível de dificuldade em relação às práticas iniciais da disciplina ao introduzir um protocolo de roteamento dinâmico clássico baseado em **vetor-distância**. A atividade permite ao aluno observar não apenas a configuração do **RIPv2**, mas também o comportamento da rede diante de uma mudança de topologia.

Ao analisar a propagação de rotas, o desaparecimento de caminhos e o tempo necessário para a rede atingir um novo estado estável, o estudante compreende limitações importantes do RIP, como **convergência lenta**, dependência de temporizadores e vulnerabilidade a problemas como **count to infinity**. A prática também prepara o terreno para comparações futuras com protocolos de convergência mais rápida, como o **OSPF**.

---

## 3. Objetivos

Ao final da atividade, o aluno deverá ser capaz de:

- configurar o **RIPv2** em uma topologia com três roteadores;
- anunciar redes diretamente conectadas;
- verificar tabelas de roteamento e parâmetros do protocolo RIP;
- observar o comportamento da rede após a queda de um enlace;
- medir e interpretar o **tempo de convergência**;
- analisar o impacto de mecanismos como **split horizon**, **poison reverse** e **triggered updates**;
- relacionar a prática com as limitações do RIP em redes maiores.

---

## 4. Fundamentação teórica

Protocolos de roteamento dinâmico foram desenvolvidos para permitir que roteadores descubram, atualizem e removam rotas automaticamente, reduzindo a necessidade de configuração manual em redes com múltiplos caminhos e mudanças frequentes. Entre esses protocolos, o **RIP - Routing Information Protocol** ocupa lugar importante na história das redes IP por sua simplicidade de operação e valor didático. Mesmo sendo considerado limitado para redes modernas de maior porte, ele continua sendo extremamente útil em laboratório por permitir a observação clara de conceitos fundamentais como troca de rotas, atualização periódica, métrica por saltos e convergência.

O RIP pertence à classe dos protocolos de **vetor-distância**. Nesse modelo, cada roteador anuncia periodicamente a seus vizinhos as redes que conhece e a distância até elas, medida em **número de saltos**. Cada roteador, ao receber essas informações, recalcula sua tabela de roteamento e escolhe o melhor caminho com base na menor métrica. No RIP, uma rota com até **15 saltos** é considerada alcançável; uma métrica **16** representa destino inalcançável. Essa característica torna o protocolo simples, mas também limita sua aplicação a redes pequenas.

### Diagrama explicativo do funcionamento do RIP

```mermaid
flowchart LR
    classDef host fill:#bbdefb,stroke:#1565c0,stroke-width:2,color:#111;
    classDef router fill:#ffe0b2,stroke:#ef6c00,stroke-width:2,color:#111;
    classDef note fill:#f5f5f5,stroke:#616161,stroke-dasharray: 5 5,color:#111;
    classDef fail fill:#ffcdd2,stroke:#c62828,stroke-width:2,color:#111;

    LAN1["💻 LAN 1<br/>192.168.10.0/24"]:::host
    R1["📡 R1<br/>Aprende rotas RIP"]:::router
    R2["📡 R2<br/>Troca anúncios a cada período"]:::router
    R3["📡 R3<br/>Aprende rotas RIP"]:::router
    LAN3["💻 LAN 3<br/>192.168.30.0/24"]:::host

    N1["Atualizações periódicas<br/>com número de saltos"]:::note
    N2["Falha de enlace<br/>altera a convergência"]:::fail
    N3["Métrica 16 =<br/>rota inalcançável"]:::note

    LAN1 --> R1
    R1 <-->|"RIPv2"| R2
    R2 <-->|"RIPv2"| R3
    R3 --> LAN3

    R2 --> N1
    R2 -. falha .-> N2
    R3 --> N3
```
O funcionamento do RIP depende da troca regular de informações entre roteadores vizinhos. No RIPv1, essas atualizações eram enviadas por broadcast, enquanto o RIPv2 introduziu melhorias importantes, como suporte a CIDR/VLSM, autenticação e envio por multicast, tornando o protocolo mais adequado a ambientes IPv4 contemporâneos. Ainda assim, a lógica de vetor-distância foi mantida, o que preserva suas limitações estruturais.

Um dos conceitos mais importantes para compreender o comportamento do RIP é o de convergência. Diz-se que a rede convergiu quando todos os roteadores possuem uma visão consistente e atualizada da topologia. Em situação estável, isso significa que todas as tabelas de roteamento refletem corretamente os melhores caminhos disponíveis. Quando ocorre uma falha de enlace, porém, essa consistência não é restaurada imediatamente. Cada roteador precisa detectar a mudança, propagar a nova informação e recalcular suas rotas. Esse processo pode levar tempo, especialmente em protocolos de vetor-distância como o RIP.

A lentidão da convergência do RIP está relacionada ao uso de temporizadores e ao modo como as informações se propagam pela rede. Como os anúncios são periódicos, pode haver atraso entre a ocorrência da falha e sua percepção pelos demais roteadores. Durante esse intervalo, alguns dispositivos ainda podem acreditar que o caminho antigo continua válido, o que gera inconsistências temporárias. Em laboratório, esse comportamento é particularmente útil porque permite ao aluno observar, na prática, a diferença entre uma rede operando em estado estável e uma rede em processo de adaptação a uma mudança de topologia.

Outro fenômeno clássico associado ao RIP é o problema de count to infinity. Esse problema ocorre quando roteadores trocam informações incorretas sobre uma rede que deixou de existir, aumentando gradualmente a métrica até que ela atinja o valor 16, considerado infinito no contexto do protocolo. Esse comportamento pode prolongar a convergência e gerar loops temporários. Para reduzir esse tipo de problema, o RIP incorpora mecanismos como split horizon, poison reverse e triggered updates. O split horizon evita que uma rota aprendida por uma interface seja anunciada de volta por essa mesma interface. O poison reverse marca explicitamente uma rota como inalcançável ao reenviá-la. Já os triggered updates permitem acelerar a propagação de mudanças sem depender exclusivamente do próximo ciclo periódico de atualização.


<img width="1448" height="1086" alt="ChatGPT Image 3 de jun  de 2026, 18_44_29" src="https://github.com/user-attachments/assets/9e08fb19-31e2-40d9-9bfc-8a3117ad80e8" />



> IMPORTANTE> RIP utiliza **UDP porta 520** para o envio de atualizações. Isso reforça a ideia de que protocolos de roteamento também operam sobre camadas e mecanismos bem definidos da pilha TCP/IP. o roteamento dinâmico não é apenas uma configuração isolada, mas parte do comportamento sistêmico da rede.

---

## 5. Topologia proposta

```mermaid
flowchart LR
    PC1["💻 VPC1<br/>192.168.10.10/24"] --- R1["📡 R1<br/>G0/0: 192.168.10.1/24<br/>G0/1: 10.0.12.1/30"]
    R1 --- R2["📡 R2<br/>G0/0: 10.0.12.2/30<br/>G0/1: 10.0.23.1/30"]
    R2 --- R3["📡 R3<br/>G0/0: 10.0.23.2/30<br/>G0/1: 192.168.30.1/24"]
    R3 --- PC3["💻 VPC2<br/>192.168.30.10/24"]
```

---

## 6. Endereçamento IP

| Dispositivo | Interface | Endereço IP   | Máscara           | Gateway        |
|-------------|:-----------:|---------------|-------------------|:----------------:|
| R1          | G0/0      | 192.168.10.1  | 255.255.255.0     | -              |
| R1          | G0/1      | 10.0.12.1     | 255.255.255.252   | -              |
| R2          | G0/0      | 10.0.12.2     | 255.255.255.252   | -              |
| R2          | G0/1      | 10.0.23.1     | 255.255.255.252   | -              |
| R3          | G0/0      | 10.0.23.2     | 255.255.255.252   | -              |
| R3          | G0/1      | 192.168.30.1  | 255.255.255.0     | -              |
| VPC1        | -      | 192.168.10.10 | 255.255.255.0     | 192.168.10.1   |
| VPC2        | -      | 192.168.30.10 | 255.255.255.0     | 192.168.30.1   |

---

## 7. Montagem do cenário no PNetLab

Adicionar ao laboratório:

- **3 roteadores Cisco** com suporte a RIP;
- **2 hosts VPCs**;
- enlaces ponto a ponto entre os roteadores.

### Conexões da topologia

- conectar o **VPC1** à interface **G0/0** do **R1**;
- conectar a interface **G0/1** do **R1** à interface **G0/0** do **R2**;
- conectar a interface **G0/1** do **R2** à interface **G0/0** do **R3**;
- conectar o **VPC2** à interface **G0/1** do **R3**.

### Resultado esperado da montagem

Ao final da montagem, o cenário deverá permitir:

- conectividade entre cada host e seu gateway local;
- troca de rotas dinâmicas entre os roteadores;
- comunicação fim a fim entre as duas LANs;
- observação do comportamento da rede após uma falha de enlace.

---

## 8. Configuração básica dos hosts 

### VPC1


```bash
ip 192.168.10.10/24 192.168.10.1
save
```

### VPC2

```bash
ip 192.168.30.10/24 192.168.30.1
save
```

---

## 9. Configuração dos roteadores

### R1

```bash
enable
configure terminal
hostname R1
no ip domain-lookup

interface g0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

interface g0/1
 ip address 10.0.12.1 255.255.255.252
 no shutdown
exit

router rip
 version 2
 no auto-summary
 network 192.168.10.0
 network 10.0.12.0
end
copy running-config startup-config
```

### R2

```bash
enable
configure terminal
hostname R2
no ip domain-lookup

interface g0/0
 ip address 10.0.12.2 255.255.255.252
 no shutdown
exit

interface g0/1
 ip address 10.0.23.1 255.255.255.252
 no shutdown
exit

router rip
 version 2
 no auto-summary
 network 10.0.12.0
 network 10.0.23.0
end
copy running-config startup-config
```

### R3

```bash
enable
configure terminal
hostname R3
no ip domain-lookup

interface g0/0
 ip address 10.0.23.2 255.255.255.252
 no shutdown
exit

interface g0/1
 ip address 192.168.30.1 255.255.255.0
 no shutdown
exit

router rip
 version 2
 no auto-summary
 network 10.0.23.0
 network 192.168.30.0
end
copy running-config startup-config
```

---

## 10. Verificação inicial

Em cada roteador, executar:

```bash
show ip interface brief
show ip route
show ip protocols
```

No **VPC1**, testar a comunicação fim a fim:

```bash
ping 192.168.30.10
```

---

## 11. Experimento de convergência

### Etapa 1 - Estado estável

Com a rede funcionando:

- verificar a rota para `192.168.30.0/24` em **R1**;
- verificar a rota para `192.168.10.0/24` em **R3**;
- confirmar a conectividade entre **VPC1** e **VPC2**.

### Etapa 2 - Falha de enlace

Desativar a interface entre **R2** e **R3**.

No **R2**:

```bash
configure terminal
interface g0/1
shutdown
end
```

### Etapa 3 - Observação

Após a falha:

- repetir `show ip route` em **R1**, **R2** e **R3**;
- testar `ping 192.168.30.10` a partir do **VPC1**;
- registrar em quanto tempo a rota deixa de ser utilizável;
- observar quando a rede atinge novo estado estável.

---

## 12. Comandos de observação sugeridos

```bash
show ip route rip
show ip protocols
debug ip rip
```

> O comando `debug ip rip` deve ser usado com cautela, pois gera saída contínua no console do roteador.

---

## 13. Checklist de validação

- [ ] Topologia criada corretamente no PNetLab  
- [ ] Interfaces dos roteadores configuradas com os endereços corretos  
- [ ] Hosts VPC configurados com IP e gateway corretos  
- [ ] RIPv2 habilitado nos três roteadores  
- [ ] Comando `no auto-summary` aplicado  
- [ ] Rotas RIP visíveis nas tabelas de roteamento  
- [ ] Comunicação fim a fim funcionando antes da falha  
- [ ] Falha de enlace simulada corretamente entre R2 e R3  
- [ ] Alterações na tabela de rotas observadas após a falha  
- [ ] Tempo de convergência registrado  
- [ ] Configurações salvas com sucesso  

---

## 14. Questões para análise

1. Qual foi o tempo aproximado de convergência após a falha do enlace?
2. Quais rotas deixaram de aparecer na tabela de roteamento após a interrupção?
3. O que aconteceu com o tráfego entre as redes `192.168.10.0/24` e `192.168.30.0/24` após a falha?
4. Como o RIP representa uma rota inalcançável?
5. Por que o RIP tende a convergir mais lentamente do que protocolos como o OSPF?
6. Qual a importância dos mecanismos de **split horizon**, **poison reverse** e **triggered updates**?
7. Em que tipo de cenário real o RIP deixaria de ser uma escolha adequada?

---

## 15. Desafio extra

Para elevar ainda mais a dificuldade, monte uma versão alternativa com **topologia redundante**:

```mermaid
flowchart LR
    R1["📡 R1"] --- R2["📡 R2"]
    R2 --- R3["📡 R3"]
    R1 --- R3
```

Depois:

- anunciar as mesmas LANs;
- derrubar um enlace;
- comparar o comportamento do RIP com e sem caminho alternativo;
- verificar se a rede encontra nova rota e quanto tempo leva.

---

## 16. Entrega

O aluno deverá entregar:

- captura de tela da topologia montada no PNetLab;
- configurações de **R1**, **R2** e **R3**;
- saídas de `show ip route` antes e depois da falha;
- evidência do `ping` antes e depois da falha;
- breve análise do tempo de convergência observado.

---

## 17. Conclusão

Este laboratório amplia a complexidade das práticas anteriores ao introduzir um protocolo de roteamento dinâmico e a análise do comportamento da rede diante de falhas. A configuração do **RIPv2** em uma topologia com múltiplos roteadores permite ao aluno compreender como rotas são propagadas, aprendidas e removidas.

A observação do processo de convergência evidencia limitações clássicas do RIP, especialmente em relação ao tempo de adaptação a mudanças de topologia. Com isso, a atividade estabelece uma base importante para o estudo comparativo com protocolos mais modernos e eficientes, como o **OSPF**, que serão explorados em etapas posteriores da disciplina.

---

[← Anterior: Laboratório 03](lab03.md) | [Índice Geral (README)](../README.md) | [Próximo: Laboratório 05 →](lab05.md)



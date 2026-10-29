# Laboratório 10 - Firewall de pacotes sem estado (stateless)

- **Instituição:** Universidade de Brasília (UnB)
- **Departamento:** Departamento de Engenharia Elétrica (ENE)
- **Curso:** Engenharia de Redes de Comunicação
- **Disciplina:** ENE0025 - Protocolos de Transporte e Roteamento
- **Professor responsável:** Prof. Dr. Laerte Peotta de Melo
- **Tema:** Filtragem de pacotes stateless com iptables na camada de rede e transporte

---

### Material de Apoio: Podcast Latência Zero

<table>
  <tr>
    <td width="140" align="center">
      <a href="https://open.spotify.com/show/59S06LhFsKlyvfLFQCJ8fK">
        <img src="../images/latencia-zero-podcast.png" alt="Latência Zero - Engenharia de Redes da UnB" width="120">
      </a>
    </td>
    <td valign="top">
      O podcast <strong>Latência Zero</strong> apresenta discussões técnicas complementares sobre os temas da disciplina.<br><br>
      🎧 <strong>Episódio 7:</strong> <a href="https://open.spotify.com/episode/6mSMblRBIjOvmX0AgsO1ln?si=ccYN8DnmSEuR6XSJgDvBAA">Firewall com Amnésia (Stateless)</a>
    </td>
  </tr>
</table>

---

## 1. Objetivos

Implementar um **firewall de pacotes sem estado (*stateless*)** em uma máquina Linux no PNetLab, posicionada entre **duas máquinas Linux básicas** - preferencialmente **Ubuntu 24.04 LTS** - aplicando regras com `iptables` para controlar o tráfego entre duas redes distintas com base em endereço IP, protocolo e porta.

---

## 2. Introdução e Fundamentação Teórica

### 2.1 Introdução

Um **firewall de pacotes sem estado (*stateless*)** é um mecanismo de segurança que analisa os pacotes de rede individualmente e decide se eles podem ou não atravessar um determinado ponto da rede. Essa decisão é tomada com base em informações presentes no cabeçalho do pacote, como **endereço IP de origem**, **endereço IP de destino**, **protocolo** e **porta de comunicação**. Em outras palavras, ele funciona como um filtro que verifica regras previamente definidas e permite ou bloqueia o tráfego conforme essas regras.

<img width="1672" height="941" alt="Infográfico do iptables como filtro de pacotes: firewall Linux entre as redes 192.168.10.0/24 e 192.168.20.0/24 permitindo TCP 80, TCP 22 e ICMP e descartando TCP 23 e UDP 53" src="https://github.com/user-attachments/assets/81787ce4-4db1-4fe0-ba0d-6fe9ca2808ea" />

*Imagem gerada com uso de inteligência artificial (OpenAI, ChatGPT).*

No Linux, uma das ferramentas clássicas para implementar esse tipo de controle é o **iptables**. Com ele, é possível criar regras para autorizar ou negar comunicações específicas entre redes, hosts e serviços. Em um laboratório, isso permite demonstrar de forma prática como uma máquina Linux pode atuar como firewall entre dois segmentos de rede, controlando o fluxo de pacotes de maneira simples e objetiva.

Diferentemente de um firewall stateful, que acompanha o estado das conexões, o firewall de pacotes sem estado (*stateless*) analisa cada pacote de forma isolada. Por isso, o administrador precisa definir explicitamente o que será permitido e o que será bloqueado em cada direção do tráfego.

### 2.2 Regras de Políticas `iptables`

| Política | Significado | Comportamento | Exemplo | Uso mais comum |
|---|---|---|---|---|
| `ACCEPT` | Aceitar por padrão | Se o pacote não casar com nenhuma regra, ele será permitido | `sudo iptables -P FORWARD ACCEPT` | Ambientes de teste ou cenários em que quase tudo é liberado |
| `DROP` | Bloquear por padrão | Se o pacote não casar com nenhuma regra, ele será descartado silenciosamente | `sudo iptables -P FORWARD DROP` | Firewalls mais seguros, em que só passa o que foi explicitamente permitido |

### 2.3 Cadeias onde essas políticas são aplicadas

| Cadeia | Função |
|---|---|
| `INPUT` | Tráfego destinado ao próprio host |
| `OUTPUT` | Tráfego gerado pelo próprio host |
| `FORWARD` | Tráfego que atravessa o host, como em roteadores e firewalls |

### 2.4 Exemplo prático

| Comando | Efeito |
|---|---|
| `sudo iptables -P INPUT DROP` | Bloqueia por padrão o tráfego que chega ao host |
| `sudo iptables -P OUTPUT ACCEPT` | Permite por padrão o tráfego gerado pelo host |
| `sudo iptables -P FORWARD DROP` | Bloqueia por padrão o tráfego que atravessa o firewall |

### 2.5 Observação importante

No uso prático, a política mais recomendada para firewall costuma ser:

- `DROP` como padrão
- regras `ACCEPT` apenas para o que realmente deve passar

Isso segue a lógica de **negar tudo e liberar somente o necessário**.

> **Observação:** no Ubuntu 24.04 LTS, o comando `iptables` utiliza por padrão o *backend* `nf_tables` (pacote `iptables-nft`). A sintaxe das regras permanece a mesma, mas as regras ficam armazenadas na infraestrutura `nftables` do núcleo.

### 2.6 Principais comandos do `iptables`

| Comando | Função principal | Exemplo | Explicação |
|---|---|---|---|
| `iptables -L -n -v` | Listar regras | `sudo iptables -L -n -v` | Mostra as regras ativas, a política padrão de cada cadeia e os contadores de pacotes e bytes. |
| `iptables -S` | Exibir regras em formato textual | `sudo iptables -S` | Mostra as regras em uma forma parecida com a sintaxe usada para criá-las. |
| `iptables -A` | Adicionar regra ao final | `sudo iptables -A FORWARD -p icmp -j ACCEPT` | Acrescenta uma nova regra ao final da cadeia escolhida. |
| `iptables -I` | Inserir regra em posição específica | `sudo iptables -I FORWARD 1 -p tcp --dport 23 -j DROP` | Insere a regra em uma posição definida, útil quando a ordem das regras importa. |
| `iptables -D` | Apagar regra | `sudo iptables -D FORWARD 3` | Remove uma regra da cadeia, normalmente pelo número da linha ou repetindo a sintaxe completa. |
| `iptables -P` | Definir política padrão | `sudo iptables -P FORWARD DROP` | Define o comportamento padrão da cadeia quando nenhum pacote corresponder às regras existentes. |
| `iptables -F` | Limpar regras | `sudo iptables -F` | Remove todas as regras das cadeias padrão. |
| `iptables -X` | Remover cadeias personalizadas | `sudo iptables -X` | Apaga cadeias criadas manualmente pelo administrador. |
| `iptables -Z` | Zerar contadores | `sudo iptables -Z` | Reinicia os contadores de pacotes e bytes das regras. |
| `iptables -N` | Criar cadeia personalizada | `sudo iptables -N BLOQUEIOS` | Cria uma nova cadeia para organizar melhor as regras. |
| `-j ACCEPT` | Permitir tráfego | `sudo iptables -A FORWARD -p tcp --dport 80 -j ACCEPT` | Define que o pacote correspondente à regra será aceito. |
| `-j DROP` | Bloquear tráfego | `sudo iptables -A FORWARD -p tcp --dport 23 -j DROP` | Define que o pacote correspondente à regra será descartado. |
| `--dport` | Filtrar porta de destino | `sudo iptables -A FORWARD -p tcp --dport 80 -j ACCEPT` | Permite criar regras com base na porta de destino. |
| `--sport` | Filtrar porta de origem | `sudo iptables -A FORWARD -p tcp --sport 80 -j ACCEPT` | Permite criar regras com base na porta de origem. |
| `-s` | Definir IP de origem | `sudo iptables -A FORWARD -s 192.168.10.10 -j ACCEPT` | Filtra pacotes pelo endereço de origem. |
| `-d` | Definir IP de destino | `sudo iptables -A FORWARD -d 192.168.20.10 -j ACCEPT` | Filtra pacotes pelo endereço de destino. |
| `-p` | Definir protocolo | `sudo iptables -A FORWARD -p icmp -j ACCEPT` | Permite aplicar a regra apenas a um protocolo, como `icmp`, `tcp` ou `udp`. |

### 2.7 Principais parâmetros de `/proc/sys/net/ipv4`

| Parâmetro | O que controla | Valores comuns | Interpretação prática |
|---|---|---|---|
| `/proc/sys/net/ipv4/ip_forward` | Encaminhamento de pacotes IPv4 entre interfaces | `0`, `1` | `0` desabilita o roteamento; `1` permite que o Linux atue como roteador, gateway ou firewall entre redes |
| `/proc/sys/net/ipv4/icmp_echo_ignore_all` | Resposta a requisições ICMP Echo (ping) | `0`, `1` | `0` permite responder a ping; `1` faz o host ignorar requisições de ping IPv4 |
| `/proc/sys/net/ipv4/conf/all/rp_filter` | Reverse Path Filtering | `0`, `1`, `2` | Ajuda a reduzir spoofing. Pode afetar cenários com roteamento assimétrico, VPN e multi-homing |
| `/proc/sys/net/ipv4/conf/all/accept_redirects` | Aceitação de redirecionamentos ICMP | `0`, `1` | Em servidores e firewalls normalmente fica em `0` por segurança |
| `/proc/sys/net/ipv4/conf/all/send_redirects` | Envio de redirecionamentos ICMP | `0`, `1` | Em máquinas que atuam como firewall ou roteador Linux, costuma-se desabilitar para reduzir comportamento indesejado |
| `/proc/sys/net/ipv4/conf/all/log_martians` | Registro de pacotes suspeitos | `0`, `1` | Útil para troubleshooting e detecção de tráfego anômalo ou spoofing |
| `/proc/sys/net/ipv4/icmp_echo_ignore_broadcasts` | Resposta a ICMP broadcast | `0`, `1` | Evita resposta a pings broadcast, o que ajuda na proteção básica contra abusos |
| `/proc/sys/net/ipv4/tcp_syncookies` | Proteção contra SYN flood | `0`, `1` | Relevante para hosts e serviços expostos à rede |
| `/proc/sys/net/ipv4/conf/all/proxy_arp` | Proxy ARP | `0`, `1` | Usado em cenários específicos de roteamento, transição e integração entre segmentos |
| `/proc/sys/net/ipv4/conf/all/arp_ignore` | Política de resposta ARP | `0` a `8` | Importante em hosts com múltiplas interfaces, balanceamento e alta disponibilidade |
| `/proc/sys/net/ipv4/conf/all/arp_announce` | Forma de anúncio ARP | `0`, `1`, `2` | Ajuda a evitar respostas ARP incorretas em ambientes com várias interfaces e redes |
| `/proc/sys/net/ipv4/ip_local_port_range` | Faixa de portas efêmeras | dois números | Útil em troubleshooting de conexões, NAT e aplicações com muitas sessões simultâneas |
| `/proc/sys/net/ipv4/tcp_fin_timeout` | Tempo de espera para conexões TCP em encerramento | valor numérico | Pode ser ajustado em servidores com grande volume de conexões |
| `/proc/sys/net/ipv4/tcp_keepalive_time` | Tempo até envio de keepalive TCP | valor numérico | Útil em sessões persistentes, túneis e monitoramento de conexões ociosas |
| `/proc/sys/net/ipv4/conf/all/secure_redirects` | Aceitação segura de redirects ICMP | `0`, `1` | Relevante em *hardening* de servidores e hosts administrativos |

### 2.8 Observações rápidas

- `ip_forward` é um dos parâmetros mais importantes quando o Linux atua como **roteador**, **gateway**, **NAT** ou **firewall entre redes**.
- `rp_filter`, `accept_redirects`, `send_redirects` e `log_martians` são muito usados em **hardening** e **troubleshooting**.
- `arp_ignore` e `arp_announce` aparecem bastante em cenários com **múltiplas interfaces**, **clusters**, **VRRP/Keepalived**, **balanceamento** e **alta disponibilidade**.
- `tcp_syncookies`, `tcp_fin_timeout` e `tcp_keepalive_time` são úteis para quem administra **servidores**, **firewalls Linux** e **appliances de rede**.

### 2.9 Exemplo de ajuste temporário com `sysctl`

```bash
sudo sysctl -w net.ipv4.ip_forward=1
sudo sysctl -w net.ipv4.conf.all.accept_redirects=0
sudo sysctl -w net.ipv4.conf.all.send_redirects=0
sudo sysctl -w net.ipv4.tcp_syncookies=1
```

### 2.10 Exemplo de configuração persistente

> Editar e descomentar as linhas correspondentes em `/etc/sysctl.conf` (ou criar um arquivo em `/etc/sysctl.d/`) e aplicar com `sudo sysctl -p`.

```conf
net.ipv4.ip_forward = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.all.log_martians = 1
net.ipv4.tcp_syncookies = 1
```

### 2.11 Síntese

De forma resumida, o `iptables` permite transformar uma máquina Linux em um **firewall de pacotes sem estado (*stateless*)**, no qual cada regra determina quais pacotes podem passar e quais devem ser bloqueados. Isso torna o laboratório bastante útil para mostrar, na prática, como o controle de tráfego pode ser feito em redes reais.

> **Importante:** neste laboratório, a máquina Linux central atuará como **roteador e firewall** entre duas redes, utilizando preferencialmente o **Ubuntu Server 24.04 LTS** (`linux-ubuntu-24.04-server`).
>
> As máquinas das extremidades também serão instâncias Linux, preferencialmente **Ubuntu Server 24.04 LTS**.
>
> O foco desta prática é o **firewall de pacotes sem estado (*stateless*)**, portanto as regras serão baseadas em:
>
> - endereço IP de origem;
> - endereço IP de destino;
> - protocolo;
> - porta.
>
> Neste primeiro momento, **não será usada inspeção stateful**. A comparação com firewall stateful será feita no Laboratório 11.

### 2.12 Funcionamento interno: caminho do pacote no Netfilter

O `iptables` configura o *framework* Netfilter do núcleo Linux. Um pacote percorre pontos de interceptação (*hooks*) em que as cadeias são avaliadas. Para tráfego que apenas atravessa o firewall, como neste laboratório, aplica-se a cadeia `FORWARD`:

```mermaid
flowchart LR
    IN["Pacote recebido"] --> PRE["PREROUTING"]
    PRE --> RD{"Destino é o próprio host?"}
    RD -- "Sim" --> INPUT["INPUT"] --> LOCAL["Processo local"]
    RD -- "Não" --> FWD["FORWARD"] --> POST["POSTROUTING"] --> OUT["Pacote encaminhado"]
    LOCAL --> OUTPUT["OUTPUT"] --> POST
```

As regras de uma cadeia são avaliadas em ordem, e a primeira regra que corresponde ao pacote determina a ação; se nenhuma corresponder, aplica-se a política padrão da cadeia.

### 2.13 Exemplo concreto

A regra `iptables -A FORWARD -s 192.168.10.10 -d 192.168.20.10 -p tcp --dport 80 -j ACCEPT` casa pacotes TCP do Cliente 1 destinados à porta 80 do Cliente 2. Como o filtro não tem estado, a resposta do servidor (TCP com porta de origem 80 e destino em uma porta efêmera do Cliente 1) só é permitida porque existe uma regra explícita no sentido inverso (`--sport 80`).

### 2.14 Protocolos e portas utilizados nos testes

| Protocolo | Camada OSI | Camada TCP/IP | Transporte / porta | Especificação |
|---|---|---|---|---|
| ICMP | 3 (Rede) | Internet | IP protocolo 1 | [**RFC 792**](https://datatracker.ietf.org/doc/html/rfc792) |
| HTTP | 7 (Aplicação) | Aplicação | TCP 80 | [**RFC 9110**](https://datatracker.ietf.org/doc/html/rfc9110) e [**RFC 9112**](https://datatracker.ietf.org/doc/html/rfc9112) |
| Telnet | 7 (Aplicação) | Aplicação | TCP 23 | [**RFC 854**](https://datatracker.ietf.org/doc/html/rfc854) |
| TCP | 4 (Transporte) | Transporte | - | [**RFC 9293**](https://datatracker.ietf.org/doc/html/rfc9293) |

---

## 3. Topologia e Cenário

### 3.1 Situação-problema

Uma organização deseja controlar o tráfego entre uma rede interna e uma rede externa utilizando uma máquina Linux como firewall. O objetivo é permitir apenas alguns tipos de comunicação entre os segmentos, bloqueando acessos indevidos e analisando o comportamento do tráfego quando as regras são aplicadas no roteamento entre as redes.

### 3.2 Topologia lógica

```mermaid
flowchart LR
    HOST1["Linux Cliente 1<br/>Ubuntu 24.04 LTS<br/>192.168.10.10/24"]
    FW["Linux Firewall<br/>Ubuntu-24.04-server<br/>eth0: 192.168.10.1/24<br/>eth1: 192.168.20.1/24"]
    HOST2["Linux Cliente 2<br/>Ubuntu 24.04 LTS<br/>192.168.20.10/24"]

    HOST1 --- FW
    FW --- HOST2

    classDef host fill:#fef3c7,stroke:#d97706,color:#111827,stroke-width:1.5px;
    classDef fw fill:#dbeafe,stroke:#1d4ed8,color:#111827,stroke-width:2px;

    class HOST1,HOST2 host;
    class FW fw;
```

### 3.3 Plano de endereçamento

| Dispositivo | Interface | Endereço IP | Máscara | Gateway |
|---|---|---|---|---|
| Linux Cliente 1 | eth0 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| Linux Firewall | eth0 | 192.168.10.1 | 255.255.255.0 | - |
| Linux Firewall | eth1 | 192.168.20.1 | 255.255.255.0 | - |
| Linux Cliente 2 | eth0 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |

### 3.4 Premissas do laboratório

Neste laboratório, o foco será:

- configurar IP nas interfaces;
- ativar o roteamento IP no Linux firewall;
- criar regras de firewall com `iptables`;
- testar conectividade e bloqueios.

---

## 4. Roteiro Prático Passo a Passo

### 4.1 Configuração dos hosts Linux

#### 4.1.1 Configuração no PNetLab

```text
Image: linux-ubuntu-24.04-server
Ethernet: 1
MTU: 1500
CPU: 1
RAM: 2048 MB
Console: VNC
Qemu Arch: x86_64
Qemu NIC: virtio-net-pci
TPM: Disabled
UEFI: desmarcado
Qemu options: -machine type=pc,accel=kvm -vga virtio -usbdevice tablet -boot order=cd -cpu host -k pt-br
```

> **Credenciais padrão (Ubuntu Server):** login: `user` | senha: `Test123` (ou conforme a imagem utilizada).  
> Caso sejam utilizadas distribuições Linux alternativas leves (como Tiny Core ou Alpine Linux), a sintaxe de comandos de rede com `ip` permanece a mesma.
>
> Os nomes de interface (`eth0`, `eth1`) são usados em todo o roteiro. No Ubuntu 24.04, os nomes podem diferir (por exemplo, `ens3`), conforme a imagem; confirmar com `ip -br link` e adaptar os comandos.

#### 4.1.2 Linux Cliente 1

Configure o endereço IP e a rota padrão:

```bash
sudo ip addr add 192.168.10.10/24 dev eth0
sudo ip link set eth0 up
sudo ip route add default via 192.168.10.1
```

#### 4.1.3 Linux Cliente 2

Configure o endereço IP e a rota padrão:

```bash
sudo ip addr add 192.168.20.10/24 dev eth0
sudo ip link set eth0 up
sudo ip route add default via 192.168.20.1
```

> Em algumas imagens Linux, pode ser necessário remover endereços pré-existentes antes da configuração. Exemplo:
>
> ```bash
> sudo ip addr flush dev eth0
> ```

### 4.2 Configuração básica da máquina Linux Firewall

#### 4.2.1 Configuração no PNetLab

> Para configurar corretamente o teclado ABNT2 use o qemu options: `-machine type=pc,accel=kvm -vga virtio -usbdevice tablet -boot order=cd -cpu host -k pt-br`

```text
Image: linux-ubuntu-24.04-server
Ethernet: 2
MTU: 1500
CPU: 2
RAM: 4096 MB
Console: VNC
Qemu Arch: x86_64
Qemu NIC: virtio-net-pci
TPM: Disabled
UEFI: desmarcado
Qemu options: -machine type=pc,accel=kvm -vga virtio -usbdevice tablet -boot order=cd -cpu host -k pt-br
```

#### 4.2.2 Configuração dos endereços IP das interfaces da máquina Linux central

> **ATENÇÃO** credenciais utilizadas  
> Ubuntu login: **user**  
> password: **Test123**  

```bash
sudo ip addr add 192.168.10.1/24 dev eth0
sudo ip addr add 192.168.20.1/24 dev eth1
sudo ip link set eth0 up
sudo ip link set eth1 up
```

Verifique a configuração:

```bash
ip addr show
```

### 4.3 Ativação do roteamento IP

Para que a máquina Linux firewall encaminhe pacotes entre as duas redes, é necessário ativar o roteamento IPv4.

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

Para confirmar:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

O valor esperado é:

```text
1
```

#### 4.3.1 Configuração persistente

Editar o arquivo e descomentar (ou acrescentar) a linha `net.ipv4.ip_forward = 1`:

```bash
sudo vi /etc/sysctl.conf
```

Aplicar a configuração sem reiniciar:

```bash
sudo sysctl -p
```

### 4.4 Bloqueio de ping com `sysctl`

Além do uso do `iptables`, o Linux permite alterar o comportamento da pilha de rede com `sysctl`. Nesta etapa, será feito um teste simples para impedir que o firewall responda a requisições de ping.

```bash
sudo sysctl -w net.ipv4.icmp_echo_ignore_all=1
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```

Valor esperado:

```text
1
```

Teste a partir dos clientes:

```bash
ping 192.168.10.1
ping 192.168.20.1
```

No servidor Firewall executar o comando `tcpdump -i any -n icmp`  e observar o resultado.

Resultado esperado: **o firewall não deve responder ao ping**.

> **Observação:** essa configuração bloqueia apenas a resposta de ping destinada ao próprio firewall. Ela não substitui as regras de `iptables` e não bloqueia, por si só, o encaminhamento de pacotes ICMP entre as redes.

Para reverter:

```bash
sudo sysctl -w net.ipv4.icmp_echo_ignore_all=0
```

No servidor Firewall executar o comando `tcpdump -i any -n icmp`  e observar o resultado.

> Qual foi o comportamento? O que aconteceu de diferente?

### 4.5 Teste inicial sem firewall

Antes de aplicar regras, teste a conectividade básica entre os dois hosts Linux.

#### 4.5.1 A partir do Linux Cliente 1

```bash
ping 192.168.20.10
```

#### 4.5.2 A partir do Linux Cliente 2

```bash
ping 192.168.10.10
```

Se o roteamento estiver correto, os pings devem funcionar.

### 4.6 Limpeza das regras antigas

Antes de iniciar a configuração do firewall, limpe regras anteriores do `iptables`.

```bash
sudo iptables -F
sudo iptables -X
sudo iptables -Z
```

Defina a política padrão da cadeia `FORWARD` como bloqueio:

```bash
sudo iptables -P FORWARD DROP
```

### 4.7 Primeiras regras do firewall de pacotes sem estado (stateless)

Nesta etapa, será permitido apenas:

- **ICMP** do Linux Cliente 1 para o Linux Cliente 2;
- **HTTP** do Linux Cliente 1 para o Linux Cliente 2;
- tráfego de retorno correspondente a essas permissões, de forma explícita.

#### 4.7.1 Permitir ICMP entre os dois hosts

```bash
sudo iptables -A FORWARD -s 192.168.10.10 -d 192.168.20.10 -p icmp -j ACCEPT
sudo iptables -A FORWARD -s 192.168.20.10 -d 192.168.10.10 -p icmp -j ACCEPT
```

#### 4.7.2 Permitir HTTP do Cliente 1 para o Cliente 2

```bash
sudo iptables -A FORWARD -s 192.168.10.10 -d 192.168.20.10 -p tcp --dport 80 -j ACCEPT
sudo iptables -A FORWARD -s 192.168.20.10 -d 192.168.10.10 -p tcp --sport 80 -j ACCEPT
```

#### 4.7.3 Bloquear implicitamente o restante

Como a política padrão da cadeia `FORWARD` é `DROP`, qualquer outro tráfego não explicitamente permitido será bloqueado.

### 4.8 Regra adicional de bloqueio explícito

Para reforçar a visualização didática, adicione uma regra explícita de bloqueio para Telnet:

```bash
sudo iptables -A FORWARD -s 192.168.10.10 -d 192.168.20.10 -p tcp --dport 23 -j DROP
```

> **Observação:** como a política padrão já é `DROP`, essa regra não é obrigatória para o funcionamento, mas ajuda a ilustrar claramente o bloqueio de um serviço específico.

### 4.9 Salvando ou documentando as regras

Dependendo da distribuição Linux, as regras podem ser perdidas após reinicialização.  
Para fins de laboratório, o mais importante é registrar as regras configuradas.

Uma forma simples de documentação é:

```bash
sudo iptables -L -n -v
sudo iptables -S
```

---

## 5. Verificação e Diagnóstico

### 5.1 Testes práticos

#### 5.1.1 Teste de ICMP

No **Linux Cliente 1**:

```bash
ping 192.168.20.10
```

Resultado esperado: **deve funcionar**.

No **Linux Cliente 2**:

```bash
ping 192.168.10.10
```

Resultado esperado: **deve funcionar**, porque o ICMP foi liberado nos dois sentidos.

#### 5.1.2 Teste de HTTP

No **Linux Cliente 2**, suba um serviço simples na porta 80.

##### 5.1.2.1 Opção usando Python

```bash
sudo python3 -m http.server 80
```

##### 5.1.2.2 Opção usando BusyBox HTTPD

```bash
sudo busybox httpd -f -p 80
```

No **Linux Cliente 1**, teste o acesso:

```bash
curl http://192.168.20.10
```

Se o `curl` não estiver instalado:

```bash
wget -O- http://192.168.20.10
```

Resultado esperado: **deve funcionar**.

#### 5.1.3 Teste de Telnet não permitido

No **Linux Cliente 1**:

```bash
telnet 192.168.20.10 23
```

Se `telnet` não estiver disponível, pode usar:

```bash
nc -vz 192.168.20.10 23
```

Resultado esperado: **deve falhar**.

#### 5.1.4 Teste de acesso iniciado pelo Cliente 2

No **Linux Cliente 2**, tente iniciar conexão TCP para o Cliente 1 em uma porta qualquer.

Exemplo com `nc`:

```bash
nc -vz 192.168.10.10 80
```

Resultado esperado: **deve falhar**, pois não há regra permitindo esse tráfego.

### 5.2 Verificação das regras

#### 5.2.1 Listar regras com contadores

```bash
sudo iptables -L -n -v
```

#### 5.2.2 Listar regras da cadeia FORWARD

```bash
sudo iptables -L FORWARD -n -v
```

#### 5.2.3 Mostrar regras em formato detalhado

```bash
sudo iptables -S
```

#### 5.2.4 O que observar

- ordem das regras;
- política padrão da cadeia `FORWARD`;
- quantidade de pacotes que corresponderam a cada regra;
- tráfego permitido e bloqueado.

### 5.3 Interpretação da saída de `iptables -L FORWARD -n -v --line-numbers`

| Campo | Significado |
|---|---|
| `Chain FORWARD (policy DROP ...)` | Cadeia e política padrão, com contadores de pacotes e bytes descartados pela política |
| `num` | Posição da regra, usada em `-D` e `-I` |
| `pkts` / `bytes` | Pacotes e bytes que casaram com a regra; contador zerado indica que a regra nunca foi atingida |
| `target` | Ação (`ACCEPT`, `DROP`, `LOG`) |
| `prot`, `in`, `out` | Protocolo e interfaces de entrada e saída |
| `source`, `destination` | Endereços de origem e destino; portas aparecem ao final (`dpt:80`, `spt:80`) |

### 5.4 Metodologia de diagnóstico

1. **Enlace e interfaces:** `ip -br link` e `ip -br addr` nos três nós;
2. **Endereçamento e gateways:** `ping` dos clientes para a interface do firewall em suas respectivas redes;
3. **Encaminhamento:** `cat /proc/sys/net/ipv4/ip_forward` igual a `1` no firewall;
4. **Regras e ordem:** `sudo iptables -L FORWARD -n -v --line-numbers`; observar contadores antes e depois de cada teste para identificar a regra atingida (ou a política padrão);
5. **Captura:** `sudo tcpdump -i any -n host 192.168.20.10` no firewall mostra se o pacote chegou e se uma resposta foi emitida;
6. **Serviço de destino:** confirmar que o servidor está em escuta (`ss -tln`), de modo a distinguir bloqueio do firewall de ausência de serviço.

---

## 6. Segurança

### 6.1 Riscos associados

- **Regras de retorno amplas:** a regra `--sport 80` aceita qualquer pacote TCP do Cliente 2 com porta de origem 80 destinado ao Cliente 1, ainda que não faça parte de uma conexão iniciada por este. Um atacante pode forjar a porta de origem para atravessar o filtro e realizar varreduras (*ACK scan*). Essa limitação é a motivação do firewall com estado (Laboratório 11).
- **Falsificação de endereço de origem:** o filtro avalia apenas os campos do cabeçalho; nada impede pacotes com endereço de origem forjado ([**RFC 2827**](https://datatracker.ietf.org/doc/html/rfc2827)).
- **Perda de acesso de gerência:** definir `INPUT DROP` sem regras que preservem o acesso administrativo pode isolar o próprio firewall.
- **Persistência:** as regras são perdidas na reinicialização; um firewall que reinicia com política `ACCEPT` fica exposto.
- **Credenciais padrão:** a imagem utilizada possui usuário e senha padrão (`user` / `Test123`), adequados somente para o laboratório isolado.
- **Política em documentos oficiais:** o comportamento esperado de firewalls de Internet é descrito na [**RFC 2979**](https://datatracker.ietf.org/doc/html/rfc2979).

### 6.2 Boas práticas (*hardening*)

```bash
# Antes de definir a política INPUT como DROP: preservar tráfego local e acesso de gerência
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.10.10 -j ACCEPT
# Antispoofing: descarta pacotes cuja origem é incompatível com a interface de entrada (inseridas no início da cadeia)
sudo iptables -I FORWARD 1 -i eth0 ! -s 192.168.10.0/24 -j DROP
sudo iptables -I FORWARD 1 -i eth1 ! -s 192.168.20.0/24 -j DROP
# Registro de pacotes descartados, com limite de taxa para evitar inundação de logs
sudo iptables -A FORWARD -m limit --limit 5/min -j LOG --log-prefix "FW-DROP: "
# Persistência das regras entre reinicializações
sudo apt install -y iptables-persistent
sudo netfilter-persistent save
```

Recomenda-se, ainda, habilitar `rp_filter` e desabilitar `accept_redirects` e `send_redirects`, conforme a tabela da Seção 2, e alterar as credenciais padrão antes de qualquer uso fora do laboratório.

---

## 7. Questões para Análise e Discussão

### 7.1 Questões para análise

1. O que caracteriza um **firewall de pacotes sem estado (*stateless*)**?
2. Quais campos do pacote foram usados nas regras deste laboratório?
3. Por que foi necessário ativar o **IP forwarding** no Linux?
4. Qual é a função da cadeia `FORWARD` no `iptables`?
5. Por que o tráfego não permitido foi bloqueado mesmo sem regras específicas para todos os protocolos?
6. Qual a diferença entre permitir **HTTP** e permitir **ICMP**?
7. O que muda quando a política padrão da cadeia `FORWARD` é `DROP`?
8. Por que esse laboratório ainda não é considerado um firewall stateful?
9. Qual a importância da ordem das regras no `iptables`?
10. Quais vantagens práticas surgem ao usar hosts Linux básicos no lugar de VPCs neste laboratório?
11. Qual a diferença entre bloquear o ping com `sysctl` e bloquear ICMP com `iptables`?

### 7.2 Conclusão esperada

Ao final deste laboratório, o estudante deve perceber que:

- uma máquina Linux pode atuar como **firewall de pacotes sem estado (*stateless*)** entre redes distintas;
- o `iptables` permite controlar o tráfego com base em **IP, protocolo e porta**;
- o roteamento entre redes depende da ativação do **IP forwarding**;
- a política padrão de bloqueio ajuda a tornar o controle mais seguro;
- o uso de **Ubuntu Server** ou **Alpine Linux** nos hosts amplia as possibilidades de teste em comparação com VPCs simples;
- o firewall de pacotes sem estado analisa cada pacote de forma isolada, o que prepara o caminho para a comparação futura com um **firewall stateful**.

---

## 8. Critérios de Avaliação e Entregáveis

### 8.1 Critérios de avaliação

| Critério | Pontuação |
|---|---:|
| Configuração do endereçamento IP e validação da conectividade de enlace | 1,5 |
| Ativação do roteamento IP (`ip_forward`) no gateway Linux | 1,0 |
| Implementação das políticas padrão e regras de filtragem no `iptables` | 3,0 |
| Testes práticos de conectividade e bloqueio (ping, HTTP e Telnet) | 2,5 |
| Respostas técnicas às questões para análise | 2,0 |
| **Total** | **10,0** |

### 8.2 Entregáveis

Cada aluno deve entregar relatório contendo:

- print da topologia no PNetLab;
- print da configuração IP dos três Linux;
- print do comando `iptables -L -n -v`;
- evidência dos testes de:
  - ping permitido;
  - HTTP permitido;
  - Telnet bloqueado;
- relatório curto contendo:
  - objetivo do laboratório;
  - resumo das regras criadas;
  - análise do que foi permitido e do que foi bloqueado;
- respostas completas às questões para análise.

---

## 9. Referências

- [**RFC 792**](https://datatracker.ietf.org/doc/html/rfc792) - *Internet Control Message Protocol*.
- [**RFC 854**](https://datatracker.ietf.org/doc/html/rfc854) - *Telnet Protocol Specification*.
- [**RFC 2827**](https://datatracker.ietf.org/doc/html/rfc2827) - *Network Ingress Filtering* (BCP 38).
- [**RFC 2979**](https://datatracker.ietf.org/doc/html/rfc2979) - *Behavior of and Requirements for Internet Firewalls*.
- [**RFC 9110**](https://datatracker.ietf.org/doc/html/rfc9110) - *HTTP Semantics*.
- [**RFC 9112**](https://datatracker.ietf.org/doc/html/rfc9112) - *HTTP/1.1*.
- [**RFC 9293**](https://datatracker.ietf.org/doc/html/rfc9293) - *Transmission Control Protocol (TCP)*.
- Projeto Netfilter. *Documentação do iptables e do Netfilter*. Disponível em: https://www.netfilter.org/documentation/.
- Páginas de manual `iptables(8)`, `iptables-extensions(8)` e `sysctl(8)`.
- ZWICKY, E. D.; COOPER, S.; CHAPMAN, D. B. *Building Internet Firewalls*. O'Reilly.
- KUROSE, J. F.; ROSS, K. W. *Redes de Computadores e a Internet: uma abordagem top-down*. Pearson.

---

[← Anterior: Laboratório 09](lab09.md) | [Índice Geral (README)](../README.md) | [Próximo: Laboratório 11 →](lab11.md)

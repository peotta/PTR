# Instalação Completa: LineageOS + Magisk + Kali NetHunter no Xiaomi Mi 9 Lite (pyxis)

---

## 1. Compatibilidade com Outros Aparelhos

Embora este guia tenha sido elaborado utilizando um Xiaomi Mi 9 Lite (Pyxis), os procedimentos apresentados podem ser adaptados para outros smartphones Android compatíveis com LineageOS, Magisk e Kali NetHunter.

Antes de iniciar a instalação em outro dispositivo, recomenda-se verificar:

## Requisitos Mínimos

- Bootloader desbloqueável.
- Suporte oficial ou comunitário ao LineageOS.
- Suporte ao Magisk.
- Compatibilidade com Kali NetHunter Rootless ou NetHunter Full.
- Espaço livre mínimo de 15 GB para instalação do Kali.
- Pelo menos 4 GB de RAM (recomendado).
- Android 12 ou superior (preferencialmente Android 14 ou Android 15).

## Verificações Recomendadas

Consultar:

- Disponibilidade do LineageOS para o dispositivo.
- Compatibilidade do NetHunter no site oficial.
- Existência de recovery compatível (Lineage Recovery, TWRP ou OrangeFox).
- Compatibilidade do kernel com recursos avançados de segurança.
- Suporte a Monitor Mode e Packet Injection, caso o objetivo seja auditoria Wi-Fi.

## Recursos que Podem Variar Entre Dispositivos

| Recurso | Dependência |
|-----------|-------------|
| Root com Magisk | Compatibilidade do boot.img |
| Kali Chroot | Espaço disponível |
| KeX (Interface Gráfica) | Memória RAM |
| HID Attacks | Kernel e suporte USB |
| BadUSB | Kernel e hardware |
| Monitor Mode Interno | Driver Wi-Fi |
| Packet Injection | Driver Wi-Fi |
| SDR | Hardware adicional |
| USB Arsenal | Suporte OTG |

## Recomendação

Para laboratórios de redes, cibersegurança e testes educacionais, recomenda-se utilizar dispositivos com ampla documentação e suporte da comunidade, como:

- Xiaomi Mi 9 Lite (Pyxis)
- Xiaomi Poco X3 Pro
- Xiaomi Poco F3
- Xiaomi Redmi Note 10 Pro
- OnePlus 7/7T
- OnePlus 8
- Google Pixel 6
- Google Pixel 7
- Google Pixel 8

## Observação Importante

A instalação do Kali NetHunter em outros dispositivos é perfeitamente possível, desde que sejam seguidas as recomendações de compatibilidade do fabricante da ROM, do Magisk e da documentação oficial do NetHunter.

A compatibilidade dos recursos avançados (Monitor Mode, Packet Injection, HID e USB Arsenal) depende principalmente do kernel e dos drivers disponibilizados para cada aparelho.


## 1. Ambiente

### Aparelho

- Xiaomi Mi 9 Lite
- Codinome: `pyxis`
- Bootloader desbloqueado


<img width="1536" height="1024" alt="ChatGPT Image 22 de jun  de 2026, 19_16_38" src="https://github.com/user-attachments/assets/aa0b3d03-bb48-408a-9a2d-66465a69d4f7" />




### Computador

- Windows
- ADB/Fastboot em:

```cmd
E:\Downloads\platform-tools
```

### Arquivos utilizados

```text
lineage-22.2-20260616-nightly-pyxis-signed.zip
recovery.img
boot.img
Magisk-v30.7.apk
NetHunter.apk
```

---

# 2. Verificar ADB

Com o Android ligado:

```cmd
adb devices
```

Resultado esperado:

```text
fb0ee349    device
```

---

# 3. Entrar em Fastboot

```cmd
adb reboot bootloader
```

Verificar:

```cmd
fastboot devices
```

Resultado:

```text
fb0ee349    fastboot
```

Verificar bootloader:

```cmd
fastboot getvar unlocked
```

Resultado:

```text
unlocked: yes
```

---

# 4. Instalar/Inicializar Lineage Recovery

Usar o recovery oficial da mesma build do LineageOS:

```cmd
fastboot boot recovery.img
```

Se desejar gravar o recovery:

```cmd
fastboot flash recovery recovery.img
```

---

# 5. Instalar LineageOS

No Lineage Recovery:

```text
Factory reset
→ Format data / factory reset
```

Depois:

```text
Apply update
→ Apply from ADB
```

No PC:

```cmd
adb sideload lineage-22.2-20260616-nightly-pyxis-signed.zip
```

Resultado esperado:

```text
Install completed with status 0.
```

Reiniciar:

```text
Reboot system now
```

---

# 6. Primeiro Boot

Aguardar o LineageOS iniciar.

Resultado esperado:

```text
Welcome to LineageOS
```

Configurar o sistema inicial.

Verificar:

```text
Configurações
→ Sobre o dispositivo
```

Resultado esperado:

```text
Modelo: Mi 9 Lite
Android: 15
LineageOS: 22.2-20260616-NIGHTLY-pyxis
```

---

# 7. Ativar Opções do Desenvolvedor

```text
Configurações
→ Sobre o telefone
→ Número da versão
→ Tocar 7 vezes
```

Depois:

```text
Configurações
→ Sistema
→ Opções do desenvolvedor
```

Ativar:

```text
Depuração USB
```

Verificar no PC:

```cmd
adb devices
```

---

# 8. Instalar Magisk

Instalar APK:

```cmd
adb install Magisk-v30.7.apk
```

Copiar boot original para o celular:

```cmd
adb push boot.img /sdcard/Download/
```

No Magisk:

```text
Instalar
→ Selecionar e corrigir um arquivo
→ Download/boot.img
```

O Magisk irá gerar:

```text
magisk_patched-30700_xxxxx.img
```

No PC, localizar:

```cmd
adb shell ls /sdcard/Download/magisk*
```

Copiar para o PC:

```cmd
adb pull /sdcard/Download/magisk_patched-30700_xxxxx.img
```

Entrar em Fastboot:

```cmd
adb reboot bootloader
```

Gravar boot corrigido:

```cmd
fastboot flash boot magisk_patched-30700_xxxxx.img
```

Reiniciar:

```cmd
fastboot reboot
```

---

# 9. Confirmar Magisk

Abrir Magisk.

Resultado esperado:

```text
Magisk instalado: 30.7
Ramdisk: Sim
```

Testar root:

```cmd
adb shell su -c id
```

Resultado esperado:

```text
uid=0(root) gid=0(root)
```

---

# 10. Instalar NetHunter

Instalar o APK:

```cmd
adb install NetHunter.apk
```

Abrir o aplicativo NetHunter.

Conceder permissões e root via Magisk.

---

# 11. Instalar Kali Chroot

No NetHunter:

```text
Kali Chroot Manager
→ Install
→ Download Latest Kali Chroot
```

Escolher:

```text
Minimal
```

Aguardar download e instalação.

---

# 12. Iniciar Kali

No NetHunter:

```text
Kali Chroot Manager
→ Start
```

No terminal Kali:

```bash
whoami
```

Resultado:

```text
root
```

Verificar versão:

```bash
cat /etc/os-release
```

Resultado esperado:

```text
Kali GNU/Linux Rolling
```

---

# 13. Atualizar Repositórios

Executar apenas:

```bash
apt update
```

Evitar inicialmente:

```bash
apt full-upgrade
apt dist-upgrade
kali-linux-full
kali-linux-everything
```

---

# 14. Instalar Ferramentas Top 10

```bash
apt install kali-tools-top10 -y
```

Verificar integridade:

```bash
dpkg --audit
```

Resultado ideal:

```text
sem saída
```

---

# 15. Instalar KeX

Instalar NetHunter KeX pela NetHunter Store.

No Kali:

```bash
apt install kali-win-kex
```

Iniciar:

```bash
kex
```

Verificar:

```bash
kex --status
```

---

# 16. Configurar SSH

Verificar pacotes:

```bash
dpkg -l | grep openssh
```

Gerar host keys:

```bash
ssh-keygen -A
```

Iniciar SSH:

```bash
/usr/sbin/sshd
```

Verificar porta:

```bash
ss -tlnp | grep :22
```

---

# 17. SSH via USB

No Windows:

```cmd
adb forward tcp:2222 tcp:22
```

Conectar:

```powershell
ssh root@127.0.0.1 -p 2222
```

---

# 18. Modo Monitor Wi-Fi Interno

Criar interface monitor:

```bash
iw phy phy0 interface add mon0 type monitor
```

Ativar:

```bash
ip link set mon0 up
```

Verificar:

```bash
iw dev
```

Resultado esperado:

```text
Interface mon0
type monitor
```

Testar captura:

```bash
tcpdump -i mon0
```

ou:

```bash
tshark -i mon0
```

---

# 19. Limitação com Aircrack-ng

No Mi 9 Lite, o monitor mode interno foi criado, porém o Aircrack apresentou erro:

```text
ioctl(SIOCSIWMODE) failed: Invalid argument
Error setting channel: Operation not supported (-95)
```

Conclusão:

```text
O driver Qualcomm icnss permite criar mon0, mas não oferece compatibilidade completa com Aircrack-ng.
```

---

# 20. Recomendação para Wi-Fi

Usar adaptador USB OTG compatível:

```text
ALFA AWUS036NHA - AR9271
TP-Link TL-WN722N v1 - AR9271
ALFA AWUS036ACH - RTL8812AU
```

Com adaptador USB:

```bash
airmon-ng start wlan1
airodump-ng wlan1mon
```

---

# 21. Estado Final

| Componente | Status |
|---|---|
| LineageOS 22.2 | OK |
| Android 15 | OK |
| Bootloader desbloqueado | OK |
| Magisk 30.7 | OK |
| Root | OK |
| NetHunter | OK |
| Kali Chroot Minimal | OK |
| kali-tools-top10 | OK |
| KeX | OK |
| SSH | OK |
| SSH via USB | OK |
| mon0 criado | OK |
| Aircrack Wi-Fi interno | Limitado |
| Adaptador USB Wi-Fi | Recomendado |

---

# 22. Comandos úteis

```bash
apt update
dpkg --audit
whoami
cat /etc/os-release
iw dev
ip addr
ss -tlnp
kex --status
```

---

# 23. Cuidados

Não executar logo após a instalação:

```bash
apt full-upgrade
apt dist-upgrade
apt install kali-linux-full
apt install kali-linux-everything
```

Preferir instalação gradual:

```bash
apt install nmap
apt install aircrack-ng
apt install hashcat
apt install wireshark
apt install tcpdump
```

---

[Índice Geral (README)](../README.md)


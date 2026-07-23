# linux-minimal-vm-cheatsheet

Cola rápida para instalar/configurar Linux minimal em VM.

Alternar para usuário `root` para iniciar a configuração do sistema:

```bash
su -
```

```text
**IMPORTANTE**: </br>
O comando `su` significa **substitute user** ou **switch user**. Ele alterna o contexto do usuário atual para outro sem encerrar a sessão original. 
O papel do hífen (`-`) não é mudar a ação do comando (que continua sendo *alternar*), mas alterar o **ambiente**:
* `su` (**sem hífen**): Alterna para o usuário root mantendo as variáveis de ambiente (como `$PATH` e `$HOME`) do seu usuário comum.
* `su -` (**com hífen**): Alterna para o usuário root e inicializa um login shell completo, carregando as variáveis de ambiente, os scripts de perfil (`/root/.bash_profile` ou `/root/.profile`) e definindo o diretório de trabalho inicial como `/root`.
```




## Validação básica do sistema


Mostrar resumo visual do sistema no terminal:

```bash
neofetch --no-install-recommends
neofetch
```

> **ALTERNATIVAS**: </br>
> * `sudo apt install fastfetch`: versão nova do neofetch.
> * `cat /etc/os-release`: mostra a distribuição e versão instalada.
> * `uname -r`: mostra a versão do kernel carregado.
> * `dpkg --print-architecture`: verificar arquitetura, se o sistema é 64 bits.
> * `hostnamectl`: verificar hostname da máquina.

Verificar/ajustar data e timezone:

```bash
timedatectl
timedatectl set-timezone America/Sao_Paulo
```

Verificar/definir idioma e localidade para pt-BR:

```bash
locale
update-locale LANG=pt_BR.UTF-8 LANGUAGE=pt_BR:pt:en
```

Verificar idioma, teclado e layout configurado pelo systemd:

```bash
localectl status
```

## Validação da rede

```text
Verificar conectividade com internet:
ping -c 4 8.8.8.8

Lista as interfaces de rede detectadas:
ip a

Verificar rota padrão:
ip route

Testar resolução DNS:
ping -c 4 deb.debian.org
```

# Verificar e editar os repositórios APT ativos

```text
# Mostra as fontes de pacotes configuradas.
grep -R "^[^#]" /etc/apt/sources.list /etc/apt/sources.list.d/ 2>/dev/null

# Abre o arquivo principal de repositórios do Debian:
nano /etc/apt/sources.list

# Arquivo sources.list recomendado para Debian 13 Trixie

deb http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware

deb http://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware
deb-src http://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware

deb http://deb.debian.org/debian/ trixie-updates main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ trixie-updates main contrib non-free non-free-firmware

```








</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>


# Linux Minimal VM Cheatsheet

Checklist direto para pós-instalação de uma VM Linux mínima, com foco em Debian/Ubuntu em ambiente de laboratório.

Objetivo:

```text
instalação mínima
validação inicial do sistema
configuração de repositórios
sudo
rede
ambiente gráfico opcional
VirtualBox Guest Additions
ajustes básicos de uso
```

---

# 1. Acessar como root

Entrar como root para iniciar a configuração do sistema.

```bash
su -
```

---

# 2. Verificar versão do sistema

Mostra a distribuição e versão instalada.

```bash
cat /etc/os-release
```

---

# 3. Verificar kernel em uso

Mostra a versão do kernel carregado.

```bash
uname -r
```

---

# 4. Verificar arquitetura

Confirma se o sistema é 64 bits.

```bash
dpkg --print-architecture
```

---

# 5. Verificar hostname

Mostra o nome da máquina.

```bash
hostnamectl
```

---

# 6. Verificar data e timezone

Mostra data, hora e fuso horário configurado.

```bash
timedatectl
```

---

# 7. Ajustar timezone para São Paulo

Define o fuso horário do Brasil/São Paulo.

```bash
timedatectl set-timezone America/Sao_Paulo
```

---

# 8. Verificar idioma e localidade

Mostra idioma, moeda, data, medidas e mensagens do sistema.

```bash
locale
```

---

# 9. Ajustar idioma para Português do Brasil

Define o sistema para pt-BR.

```bash
update-locale LANG=pt_BR.UTF-8 LANGUAGE=pt_BR:pt:en
```

---

# 10. Verificar teclado e localidade pelo systemd

Mostra idioma, teclado e layout configurado.

```bash
localectl status
```

---

# 11. Verificar interfaces de rede

Lista as interfaces de rede detectadas.

```bash
ip a
```

---

# 12. Verificar rota padrão

Confirma se existe gateway configurado.

```bash
ip route
```

---

# 13. Testar conectividade por IP

Testa comunicação com a internet sem depender de DNS.

```bash
ping -c 4 8.8.8.8
```

---

# 14. Testar resolução DNS

Testa se nomes de domínio estão resolvendo.

```bash
ping -c 4 deb.debian.org
```

---

# 15. Verificar repositórios APT ativos

Mostra as fontes de pacotes configuradas.

```bash
grep -R "^[^#]" /etc/apt/sources.list /etc/apt/sources.list.d/ 2>/dev/null
```

---

# 16. Editar sources.list no Debian

Abre o arquivo principal de repositórios do Debian.

```bash
nano /etc/apt/sources.list
```

---

# 17. sources.list recomendado para Debian 13 Trixie

Usar este conteúdo no Debian 13.

```text
deb http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware

deb http://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware
deb-src http://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware

deb http://deb.debian.org/debian/ trixie-updates main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ trixie-updates main contrib non-free non-free-firmware
```

---

# 18. Atualizar índice de pacotes

Atualiza a lista de pacotes disponíveis.

```bash
apt update
```

---

# 19. Atualizar pacotes instalados

Atualiza os pacotes do sistema.

```bash
apt upgrade -y
```

---

# 20. Instalar sudo

Instala o comando sudo.

```bash
apt install -y sudo
```

---

# 21. Adicionar usuário ao grupo sudo

Permite que o usuário execute comandos administrativos com sudo.

```bash
usermod -aG sudo henrique
```

---

# 22. Reiniciar após adicionar ao sudo

Aplica a associação do usuário ao grupo sudo.

```bash
reboot
```

---

# 23. Testar sudo após reiniciar

Confirma se o usuário consegue usar sudo.

```bash
sudo apt update
```

---

# 24. Instalar ferramentas básicas

Instala utilitários essenciais para administração.

```bash
sudo apt install -y curl wget nano vim git htop net-tools dnsutils lsb-release ca-certificates
```

---

# 25. Instalar ferramentas de rede

Instala comandos úteis para diagnóstico de rede.

```bash
sudo apt install -y iputils-ping traceroute nmap tcpdump
```

---

# 26. Verificar serviços ativos

Lista serviços em execução.

```bash
systemctl --type=service --state=running
```

---

# 27. Verificar serviços com falha

Mostra serviços que falharam.

```bash
systemctl --failed
```

---

# 28. Verificar uso de disco

Mostra espaço usado nas partições.

```bash
df -h
```

---

# 29. Verificar memória

Mostra uso de RAM e swap.

```bash
free -h
```

---

# 30. Verificar CPU

Mostra informações básicas do processador.

```bash
lscpu
```

---

# 31. Verificar discos

Lista discos e partições.

```bash
lsblk
```

---

# 32. Instalar GNOME mínimo no Debian

Instala ambiente gráfico GNOME enxuto.

```bash
sudo apt install -y gnome-core gdm3 network-manager network-manager-gnome gnome-terminal gnome-control-center nautilus firefox-esr gnome-tweaks
```

---

# 33. Instalar áudio moderno

Instala PipeWire e suporte básico de áudio/Bluetooth.

```bash
sudo apt install -y pipewire-audio wireplumber libspa-0.2-bluetooth bluez blueman
```

---

# 34. Instalar editor gráfico simples

Instala editor de texto gráfico.

```bash
sudo apt install -y gedit
```

---

# 35. Reiniciar após instalar desktop

Reinicia para entrar na tela gráfica.

```bash
sudo reboot
```

---

# 36. Verificar sessão gráfica

Mostra se a sessão está em X11 ou Wayland.

```bash
echo $XDG_SESSION_TYPE
```

---

# 37. Corrigir NetworkManager se a rede cabeada não aparecer

Abre a configuração do NetworkManager.

```bash
sudo nano /etc/NetworkManager/NetworkManager.conf
```

---

# 38. Ajuste no NetworkManager

Alterar a linha para permitir gerenciamento das interfaces.

```text
managed=true
```

---

# 39. Reiniciar NetworkManager

Reinicia o serviço de rede.

```bash
sudo systemctl restart NetworkManager
```

---

# 40. Instalar thumbnails para imagens e vídeos

Permite exibir miniaturas no Nautilus.

```bash
sudo apt install -y ffmpegthumbnailer libgdk-pixbuf2.0-bin
```

---

# 41. Instalar suporte a NTFS

Permite leitura e escrita em discos/pendrives NTFS.

```bash
sudo apt install -y ntfs-3g
```

---

# 42. Instalar aplicativos opcionais

Instala aplicativos úteis, mas não essenciais.

```bash
sudo apt install -y vlc shotwell cheese gnome-software
```

---

# 43. Instalar pré-requisitos do VirtualBox Guest Additions

Instala ferramentas para compilar os módulos do VirtualBox.

```bash
sudo apt install -y dkms build-essential linux-headers-$(uname -r)
```

---

# 44. Reiniciar antes do Guest Additions

Garante que o sistema está usando o kernel correto.

```bash
sudo reboot
```

---

# 45. Inserir ISO Guest Additions no VirtualBox

No menu do VirtualBox, inserir o CD dos adicionais de convidado.

```text
Dispositivos > Inserir imagem de CD dos Adicionais para Convidado
```

---

# 46. Criar ponto de montagem do CD

Cria a pasta onde a ISO será montada.

```bash
sudo mkdir -p /mnt/cdrom
```

---

# 47. Montar CD do Guest Additions

Monta a ISO do VirtualBox dentro da VM.

```bash
sudo mount /dev/cdrom /mnt/cdrom
```

---

# 48. Copiar instalador para /tmp

Copia o instalador para uma pasta gravável.

```bash
cp /mnt/cdrom/VBoxLinuxAdditions.run /tmp/
```

---

# 49. Entrar na pasta temporária

Acessa a pasta onde o instalador foi copiado.

```bash
cd /tmp
```

---

# 50. Dar permissão de execução

Permite executar o instalador.

```bash
chmod +x VBoxLinuxAdditions.run
```

---

# 51. Instalar Guest Additions

Executa a instalação dos adicionais do VirtualBox.

```bash
sudo ./VBoxLinuxAdditions.run
```

---

# 52. Reiniciar após Guest Additions

Aplica os módulos e serviços instalados.

```bash
sudo reboot
```

---

# 53. Ativar copiar e colar no VirtualBox

Configurar no menu da VM.

```text
Dispositivos > Área de transferência compartilhada > Bidirecional
```

---

# 54. Ativar arrastar e soltar no VirtualBox

Configurar no menu da VM.

```text
Dispositivos > Arrastar e soltar > Bidirecional
```

---

# 55. Adicionar usuário ao grupo vboxsf

Permite acessar pastas compartilhadas do VirtualBox.

```bash
sudo usermod -aG vboxsf $USER
```

---

# 56. Reiniciar após grupo vboxsf

Aplica a nova associação de grupo.

```bash
sudo reboot
```

---

# 57. Verificar grupos do usuário

Confirma se o usuário está no grupo vboxsf.

```bash
groups
```

---

# 58. Verificar módulos do VirtualBox na VM

Mostra módulos carregados do Guest Additions.

```bash
lsmod | grep vbox
```

---

# 59. Instalar SSH em VM Server

Instala acesso remoto por SSH.

```bash
sudo apt install -y openssh-server
```

---

# 60. Verificar status do SSH

Confirma se o serviço SSH está ativo.

```bash
systemctl status ssh
```

---

# 61. Ver IP da VM

Mostra o endereço IP para conexão SSH.

```bash
ip a
```

---

# 62. Acessar VM via SSH pelo host

Conecta na VM usando terminal do host.

```bash
ssh usuario@IP_DA_VM
```

---

# 63. Limpar pacotes desnecessários

Remove pacotes antigos que não são mais necessários.

```bash
sudo apt autoremove -y
```

---

# 64. Limpar cache do APT

Remove arquivos baixados do cache.

```bash
sudo apt clean
```

---

# 65. Checklist final

Conferir se o sistema está pronto.

```text
[ ] Sistema atualizado
[ ] sources.list correto
[ ] sudo funcionando
[ ] rede funcionando
[ ] DNS funcionando
[ ] timezone correto
[ ] locale pt_BR.UTF-8
[ ] teclado correto
[ ] GNOME instalado, se for desktop
[ ] áudio funcionando, se for desktop
[ ] Guest Additions instalado, se for VirtualBox
[ ] copiar/colar bidirecional ativo
[ ] usuário no grupo vboxsf, se usar pasta compartilhada
[ ] SSH instalado, se for server
```

---

# 66. Ordem recomendada resumida

Fluxo ideal para Debian mínimo em VM.

```text
1. verificar sistema
2. verificar rede
3. ajustar sources.list
4. atualizar sistema
5. instalar sudo
6. adicionar usuário ao sudo
7. reiniciar
8. instalar ferramentas básicas
9. instalar desktop, se necessário
10. instalar Guest Additions, se for VirtualBox
11. configurar copiar/colar e pastas compartilhadas
12. instalar SSH, se for server
13. validar sistema final
```


# 15. Verificar se o usuário está no grupo `vboxsf`


> [!IMPORTANT]
> **O papel do hífen (`-`):**
> * `su`: mantém as variáveis de ambiente (`$PATH`, `$HOME`) do usuário comum.
> * `su -`: inicializa um *login shell* completo, carregando o ambiente e o diretório `/root`.
</br>

> [!TIP]
> **O papel do hífen (`-`):**
> * `su`: mantém as variáveis de ambiente (`$PATH`, `$HOME`) do usuário comum.
> * `su -`: inicializa um *login shell* completo, carregando o ambiente e o diretório `/root`.
> * 
</br>
Outros tipos de callouts suportados:

> [!NOTE] (Azul - para notas gerais)

> [!TIP] (Verde - para dicas de boas práticas)

> [!WARNING] (Amarelo - para alertas)

> [!CAUTION] (Vermelho - para riscos/erros graves)

> Teste
> Aqui é um teste

---

> 📌 **Importante:** O hífen (`-`) altera o ambiente do shell. Enquanto `su` mantém o `$PATH` do usuário comum, `su -` carrega o ambiente completo do root (`/root`).
---

# Cola rápida para instalar/configurar Linux minimal em VM.

#### Alternar para usuário `root` para iniciar a configuração do sistema:

```bash
su -
```

#### Validar conectividade com a internet:

```bash
ping -c 4 8.8.8.8
```

# Arquivo sources.list DEBIAN 13

#### Abrir o arquivo principal de repositórios:

```bash
nano /etc/apt/sources.list
```

#### Arquivo sources.list recomendado para Debian 13 Trixie:

```bash
deb http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware

deb http://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware
deb-src http://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware

deb http://deb.debian.org/debian/ trixie-updates main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ trixie-updates main contrib non-free non-free-firmware
```

# Arquivo sources.list UBUNTU 24.04

#### Abrir o arquivo principal de repositórios:

```bash
sudo nano /etc/apt/sources.list.d/ubuntu.sources
```

#### Arquivo sources.list recomendado para Ubuntu 26.04 LTS - Resolute Raccoon:

```bash
Types: deb deb-src
URIs: http://archive.ubuntu.com/ubuntu
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb deb-src
URIs: http://security.ubuntu.com/ubuntu
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

#### Arquivo sources.list recomendado para Ubuntu 24.04 LTS - Noble Numbat:

```bash
Types: deb deb-src
URIs: http://archive.ubuntu.com/ubuntu
Suites: resolute resolute-updates resolute-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb deb-src
URIs: http://security.ubuntu.com/ubuntu
Suites: resolute-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

## Atualizar índice de pacotes

#### Atualiza a lista local de pacotes disponíveis nos repositórios configurados:

```bash
apt update
```

#### Atualiza os pacotes já instalados no sistema:

```bash
apt upgrade -y
```

---

## Instalar e habilitar o sudo

```bash
su -
apt update
apt install -y sudo
usermod -aG sudo `nome do usuário`
groups `nome do usuário`
reboot
```

#### Confirmar se o sudo está funcionando:

```bash
sudo whoami
```

---

# VirtualBox Guest Additions no Debian/Ubuntu

No menu da VM no VirtualBox, configure:

```text
Dispositivos > Área de transferência compartilhada > Bidirecional
Dispositivos > Arrastar e soltar > Bidirecional
```
#### Instalar pré-requisitos:

```bash
sudo apt update
sudo apt install -y dkms build-essential linux-headers-$(uname -r)
reboot
```

#### Inserir o CD dos Guest Additions:

```text
Dispositivos > Inserir imagem de CD dos Adicionais para Convidado
```
#### Após inserir o CD dos Guest Additions no VirtualBox:

```bash
sudo mkdir -p /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
cp /mnt/cdrom/VBoxLinuxAdditions.run /tmp/
cd /tmp
chmod +x VBoxLinuxAdditions.run
sudo ./VBoxLinuxAdditions.run
sudo reboot
```

**Atenção:**</br>
Em algumas distribuições Linux, especialmente com GNOME, o copiar e colar do VirtualBox pode falhar quando a sessão está usando Wayland. 
O VirtualBox costuma funcionar melhor com GNOME on Xorg.

## Pastas compartilhadas
Para usar pastas compartilhadas entre host e VM, é necessário adicionar o usuário ao grupo:

```bash
sudo usermod -aG vboxsf $USER
sudo reboot
```






</br>
</br>
</br>
</br>
</br>
</br>
</br>


#### Verificar/ajustar data e timezone:

```bash
timedatectl
timedatectl set-timezone America/Sao_Paulo
```

#### Verificar/definir idioma e localidade para pt-BR:

```bash
locale
update-locale LANG=pt_BR.UTF-8 LANGUAGE=pt_BR:pt:en
```

#### Verificar idioma, teclado e layout configurado pelo systemd:

```bash
localectl status
```

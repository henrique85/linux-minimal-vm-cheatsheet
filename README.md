# Cola rápida para instalar/configurar Linux minimal em VM.

Alternar para usuário `root` para iniciar a configuração do sistema:

```bash
su -
```

---

## Validação básica do sistema

#### Mostrar resumo visual do sistema no terminal:

```bash
neofetch --no-install-recommends
neofetch
```

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

---

## Validação da rede

#### Verificar conectividade com internet:

```bash
ping -c 4 8.8.8.8
```

## Verificar e editar os repositórios APT ativos

#### Abre o arquivo principal de repositórios do Debian:

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
usermod -aG sudo nome_do_usuario
groups nome_do_usuario
reboot
```

#### Confirmar se o sudo está funcionando:

```bash
sudo whoami
```

---

a




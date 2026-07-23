# Cola rápida para instalar/configurar Linux minimal em VM

## Analisar o sistema

Verificar se está com internet:
```bash
ping google.com
```

Conhecer o sistema:
```bash
neofetch --no-install-recommends
neofetch
```
---
Alternar para usuário `root`:

```bash
su -
```
Nota:</br>
O comando `su` significa **substitute user** ou **switch user**. Ele alterna o contexto do usuário atual para outro sem encerrar a sessão original. 

O papel do hífen (`-`)</br>
O hífen não muda a ação do comando (que continua sendo *alternar*), mas altera o **ambiente**:

* `su` (**sem hífen**): Alterna para o usuário root mantendo as variáveis de ambiente (como `$PATH` e `$HOME`) do seu usuário comum.

* `su -` (**com hífen**): Alterna para o usuário root e inicializa um login shell completo, carregando as variáveis de ambiente, os scripts de perfil (`/root/.bash_profile` ou `/root/.profile`) e definindo o diretório de trabalho inicial como `/root`.



</br>
---
# INSERIR DADOS ACIMA

---

# 5. Instalar pré-requisitos no Debian/Ubuntu

Dentro da VM Linux, execute:

```bash
sudo apt update
sudo apt install -y dkms build-essential linux-headers-$(uname -r)
```


## Como entrar com GNOME on Xorg

# 15. Verificar se o usuário está no grupo `vboxsf`

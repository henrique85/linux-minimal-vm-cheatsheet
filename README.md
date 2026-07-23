# linux-minimal-vm-cheatsheet
Cola rápida para instalar/configurar Linux minimal em VM

*começa aqui

---

# 5. Instalar pré-requisitos no Debian/Ubuntu

Dentro da VM Linux, execute:

```bash
sudo apt update
sudo apt install -y dkms build-essential linux-headers-$(uname -r)
```


## Como entrar com GNOME on Xorg

# 15. Verificar se o usuário está no grupo `vboxsf`

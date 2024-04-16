---
title: "Acesso Remoto a Roteadores via SSH em redes libremesh"
date: 2020-06-14
description: "Guia completo para acessar os roteador de uma rede com libremesh pela linha de comando"
image: "/images/terminal.jpg"
type: "post"
tags: ["RedesComunitarias","libremesh"]
---

Para acessar um roteador via SSH, siga os passos abaixo. Este guia assume que você está utilizando um sistema baseado em Linux, como Debian ou Ubuntu.

### Pré-requisitos

Antes de começar, é necessário ter o pacote [openssh-client](file:///home/hiure/gits/minhapagina/content/pt/posts/Como-ascessar-roteador-por-ssh.md#10%2C75-10%2C75) instalado em seu sistema. Este pacote permite que você inicie conexões SSH a partir do seu terminal.

1. **Instalação do openssh-client**

   Abra o terminal e execute o comando abaixo para atualizar os pacotes do seu sistema e instalar o [openssh-client](file:///home/hiure/gits/minhapagina/content/pt/posts/Como-ascessar-roteador-por-ssh.md#10%2C75-10%2C75):

   ```sh
   sudo apt update && sudo apt install openssh-client -y
   ```

### Conectando-se ao Roteador

2. **Acesso ao Roteador Atual**

   Para se conectar ao roteador ao qual seu computador está atualmente conectado, utilize o comando:

   ```sh
   ssh root@thisnode.info
   ```

   Substitua `root` pelo nome de usuário adequado, se necessário.

3. **Acesso a Outros Roteadores na Rede**

   - **Pelo Hostname:**

     Se você conhece o hostname do roteador ao qual deseja se conectar, use:

     ```sh
     ssh root@hostname-do-roteador
     ```

   - **Pelo IP:**

     Caso conheça o endereço IP do roteador, o comando é:

     ```sh
     ssh root@ip-do-roteador
     ```

### Descobrindo Roteadores na Rede

Se você não sabe o nome ou o IP do roteador que deseja acessar, é possível descobrir roteadores conectados na rede.

4. **Listando Roteadores pela Interface Mesh**

   - **Encontrando pelo IP:**

     Para listar os IPs dos roteadores conectados via interface mesh, enquanto conectado a um roteador via SSH, execute:

     ```sh
     ssh root@thisnode.info ip n | grep wlan0-mesh
     ```

   - **Encontrando pelo Nome:**

     Para obter os nomes, após estar conectado ao roteador via SSH, use:

     ```sh
     ip n | grep wlan0-mesh | mac2bat
     ```

     Isso mostrará uma lista de todos os roteadores conectados pela interface `wlan0-mesh`. Se essa interface não existir (por exemplo, em roteadores dual-band que não têm a interface de 2.4GHz ativada), tente usar `wlan1-mesh` ou, para roteadores específicos como o LibreRouter, `wlan2-mesh`.

     Alternativamente, você pode usar o comando `arp` para encontrar dispositivos pela interface mesh:

     ```sh
     arp | grep wlan0-mesh | mac2bat
     ```

### Notas Adicionais

- Lembre-se de substituir `root` pelo nome de usuário administrativo do roteador, se for diferente.
- Os comandos `mac2bat` e `arp` podem requerer instalação ou configuração adicional, dependendo do seu roteador e sistema operacional.

Seguindo estes passos, você será capaz de acessar roteadores na sua rede via SSH, bem como descobrir outros dispositivos conectados.


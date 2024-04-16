---
title: "Como criar uma rede Libremesh com Servidor Lokal"
date: 2023-06-14
description: "Guia completo sobre como criar uma rede mesh com Lokal como servidor para conteúdo, mídia e muito mais"
image: "/images/lokal.png"
type: "post"
tags: ["RedesComunitarias","libremesh","lokal"]
---

## Lokal 

Como parte do [projeto lokal](https://wakoma.co/lokal/), os testes com dois roteadores Archer A7 V5.8 e Unifi Mesh UAP-AC-M estão descritos abaixo


firmwares libremesh -> https://next.coolab.org/s/Eiz7r9xJKiXi8MA

### Unifi Mesh UAP-AC-M

Folha de dados Unifi -> http://dl.ubnt.com/datasheets/unifi/UniFi_AC_Mesh_DS.pdf	

Siga estes passos -> https://openwrt.org/toh/ubiquiti/unifiac?s[]=unifi&s[]=mesh#non-invasive_method_using_mtd

Breve

Vamos fazer o downgrade para uma versão mais antiga do firmware ubiquiti (ubnt.bin), instalar o firmware OpenWRT e, em seguida, instalar o firmware Libremesh.


1. Baixe o ubnt.bin da pasta

- md5sum BZ*.bin deve retornar: 5bb23b387defcbd1f6cda5819c7905e5
- mv BZ*.bin ubnt.bin

2. IP estático (192.168.1.0/24, não use IP 192.168.1.20 ou 192.168.1.1 para o computador, se não tiver certeza, use o IP 192.168.1.10, máscara de rede 255.255.255.0, gateway padrão 192.168.1.1 para o PC)

3. Copie o Firmware Unifi do seu Linux-PC para o dispositivo Unifi: scp ubnt.bin ubnt@192.168.1.20:/tmp/ (a senha també
I had a problem with traefik and transmission's password so I had to install thism é ubnt)

4. SSH no dispositivo Unifi ssh ubnt@192.168.1.20 (a senha também é ubnt)

5. No seu dispositivo Unifi, emita o comando fwupdate.real -m /tmp/ubnt.bin. Deixe o dispositivo Unifi reiniciar. 

6. scp o Firmware OpenWrt para o dispositivo Unifi scp openwrt-ath79-generic-ubnt_unifiac-XXX-squashfs-sysupgrade.bin ubnt@192.168.1.20:/tmp/

7.  SSH no dispositivo Unifi e: `mtd write /tmp/openwrt-xxxxx-squashfs-sysupgrade.bin kernel0`, depois também apague a partição não utilizada `mtd erase kernel1`

8. Descubra qual partição é chamada de “bs”: cat /proc/mtd, o resultado esperado é “mtd4”. Em seguida, emita este comando no dispositivo Unifi (use o nome da partição obtido para bs): dd if=/dev/zero bs=1 count=1 of=/dev/mtd4

9. Na próxima reinicialização, você verá um firmware openwrt.

    mude o IP estático de volta para DHCP. Desconecte e reconecte o cabo de rede.

    


10. No openwrt vá para upload de firmware e faça o upload do firmware Libremesh

    vá para o navegador. 192.168.1.1
    nome de usuário: root
    senha: vazia

    Sistema>> Voltar/Flash Firmware

    Flash Image
    Navegue até o libremesh squash
    Upload

    Deixe todas as 3 caixas desmarcadas 
    clique em continuar
    
    Após a atualização, vá para thisnode.info
    
    
11. Criar Nova Rede

Escolha um nome para rede: lokal.network
PW: Phubert pw

Choose a name for the node: uap-ac-mesh


    

### Archer A7 V5.8


1. Conecte o cabo LAN do PC à porta LAN-1 do roteador
2. Abra um navegador e acesse o endereço padrão da TP-Link http://192.168.0.1
Você será solicitado a criar uma senha na primeira abertura. Defina uma nova senha e faça login.
3. Você deverá ver a página de acesso do roteador. Selecione: Avançado/Ferramentas do Sistema/Atualização de Firmware
5. Selecione: Atualização Manual/Navegar: Selecione o arquivo baixado da seção "Instalação do Firmware OpenWrt" openwrt-22.03.5-ath79-generic-tplink_archer-a7-v5-squashfs-factory.bin
6. Aguarde até que a atualização do firmware seja concluída. Não interrompa o processo - risco de danificar o roteador!
7. Após a conclusão da atualização, você verá "página não encontrada". Isso é normal.
8. Desconecte e reconecte o cabo de rede, e abra no navegador o endereço padrão do OpenWRT: http://192.168.1.1 (configurações manuais do cartão LAN: ip4:192.168.1.122/máscara:255.255.255.0/gateway:192.168.1.1 )
9. Da atualização do OpenWRT com o Libremesh


    Sistema >> Backup/Atualização de Firmware
    Imagem de Firmware
    Navegue até librerouteros squashfs-sysupgrade.bin
    Upload

    Deixe todas as 3 caixas desmarcadas 
    clique em continuar

### Archer C7 V5


1. Conecte o cabo LAN do PC à porta LAN-1 do roteador
2. Abra um navegador e acesse o endereço padrão da TP-Link http://192.168.0.1
Você será solicitado a criar uma senha na primeira abertura. Defina uma nova senha e faça login.
3. Você deverá ver a página de acesso do roteador. Selecione: Avançado/Ferramentas do Sistema/Atualização de Firmware
5. Selecione: Atualização Manual/Navegar: Selecione o arquivo baixado da seção "Instalação do Firmware OpenWrt" openwrt-22.03.5-ath79-generic-tplink_archer-a7-v5-squashfs-factory.bin (use a versão C7 deste arquivo)
6. Aguarde até que a atualização do firmware seja concluída. Não interrompa o processo - risco de danificar o roteador!
7. Após a conclusão da atualização, você verá "página não encontrada". Isso é normal.
8. Desconecte e reconecte o cabo de rede e abra no navegador o endereço padrão do OpenWRT: http://192.168.1.1 (configurações manuais do cartão LAN: ip4:192.168.1.122/máscara:255.255.255.0/gateway:192.168.1.1 )
9. Da atualização do OpenWRT com o Libremesh
    Sistema >> Backup/Atualização de Firmware

    Imagem de Firmware
    Navegue até libremesh squashfs-sysupgrade.bin
    Upload

    Deixe todas as 3 caixas desmarcadas 
    clique em continuar


### Ansible install

python3 -m venv venv
source venv/bin/activate
pip install ansible
ansible-playbook -i hosts/preparar prepare.yml 
ansible-playbook -i hosts/nucserver.yml playbook.yml 


### Certificados

Os certificados tem sido tema para debate nos [foruns de redes comunitárias](https://communitynetworks.group/t/anyone-using-https-in-a-cn/286/26). E o melhor método para isso até agora que estamos desenvolvendo é o compartilhado pelo[ geekrewind](https://geekrewind.com/generate-free-wildcard-certificates-using-lets-encrypt-certbot-on-ubuntu-18-04/).

Os passos são:

Com o certbot instalado rode o comando:

```sudo certbot certonly --manual --preferred-challenges=dns --email hiure@riseup.net --server https://acme-v02.api.letsencrypt.org/directory --agree-tos -d redepsp.info -d *.redepsp.info```

Adicione registros txt de acordo com as instruções do certbot

```sudo certbot certificates```

```mv fullchain.pem redepsp.info.crt```

```openssl pkey -in privkey.pem -out redepsp.info.key```

Copie os certificados para a pasta do host do Ansible

`cp redepsp.info* hosts/ `

### Configurações do Ansible

Instruções - https://docs.lokal.network/gettingstarted/

Clone o repositório e remova o arquivo ansible.cfg

`git clone https://github.com/Wakoma/Lokal.git`

`rm ansible.cfg` 

rode o comando;

`ansible-galaxy install -r requirements.yml`

Edite o arquivo `hosts/preparar`

```
all:
  hosts: "10.208.191.255"
  vars:
    app_user: psp
    ansible_user: root
    setup_ssh: true
    ssh_key: ssh-rsa 
```
e rode o comando:

`ansible-playbook -i hosts/preparar prepare.yml`

Edite o arquivo `hosts/nucserver`

```
all:
  hosts: "10.208.191.255"
  vars:
    ssl_cert: "hosts/redepsp.info.cert"
    ssl_key: "hosts/redepsp.info.key"
    domain: redepsp.info
    email_admin: hiure@riseup.net
    password_admin: strong-password
    lokal_secret: nui3fhAoiSDUndakd12
    ansible_user: psp
    services:
        - kiwix
        - wordpress
        - jellyfin
        - calibre
    project_root: /home/psp
```
e rode o comando:

`ansible-playbook -i hosts/nucserver.yml playbook.yml`

#### Adicionando subdomínio ao wordpress

no arquivo `roles/wordpress/defaults/main.yml`

adicione o seu subdomio:

```subdomain_wordpress: lokal```

### Configurar o Dnsmasq

Edite o arquivo `/etc/config/lime-community` e adicione o seu domínio.

```
config lime 'system'
	option domain 'redepsp.info'

config lime 'network'

config lime 'wifi'
	option ap_ssid 'PSP'
	option apname_ssid 'PSP/%H'
```

Aplique as configurações: 

`lime-config` 

Se nenhum erro for retornado, use:

`lime-apply`

Edite o arquivo dnsmasq `/etc/dnsmasq.d/lokal.conf`

```
cname=lokal.redepsp.info,lokal
cname=wiki.redepsp.info,lokal.redepsp.info
cname=souzaflix.redepsp.info,lokal.redepsp.info
cname=biblioteca.redepsp.info,lokal.redepsp.info
cname=torrent.redepsp.info,lokal.redepsp.info
cname=router.redepsp.info,lokal.redepsp.info
```
restart dnsmasq service

`/etc/init.d/dnsmasq restart`

### Pirania config

Edite o arquivo pirania em `/etc/config/pirania` 

 - to add the destination page to redirect to, change the `option portal_domain` line to your domain and the `option url_portal` line to `/` 
 - to catch all clients, change the `list catch_interfaces`
 - to change the portal open time `option duration_m`.

Exemplo:

```
config base_config 'base_config'
	option prune_expired_for_days '30'
	option portal_domain 'lokal.redepsp.info'
	option url_auth '/portal/auth.html'
	option url_authenticated '/portal/authenticated.html'
	option url_info '/portal/info.html'
	option url_fail '/portal/fail.html'
	option db_path '/etc/pirania/vouchers/'
	option hooks_path '/etc/pirania/hooks/'
	option append_ipt_rules '0'
	list allowlist_ipv4 '10.0.0.0/8'
	list allowlist_ipv4 '172.16.0.0/12'
	list allowlist_ipv4 '192.168.0.0/16'
	list allowlist_ipv6 'fc00::/7'
	list allowlist_ipv6 'fe80::/64'
	list allowlist_ipv6 '2a00:1508:0a00::/40'
	list catch_interfaces 'br-lan'
	list catch_interfaces 'anygw'
	option enabled '1'
	option with_vouchers '0'

config access_mode 'read_for_access'
	option url_portal '/'
	option duration_m '15'
```

Depois disso rode:
`captive portal stop & captive-portal start`


## Diversos

Tive um problema com a senha do traefik e do transmission, então tive que instalar isso

`pip install --upgrade passlib`


### Nextcloud - Jellyfin integrations

jellyfin compose

```
    volumes:
      - "{{project_root}}/jellyfin/config:/config"
      - "{{project_root}}/jellyfin/data:/data"
      - "{{project_root}}/base/transmission/data:/media:ro"
      - "/media/nextcloud:/nextcloud:ro"
      
```

sudo mount --bind ~/nextcloud/data/data/admin/files/public/ /media/nextcloud



---
title: "How to create a Libremesh network with Lokal Server"
date: 2023-06-14
description: "Complete guide on how to create a mesh network with Lokal as a server for content, media, and more"
image: "/images/terminal.jpg"
type: "post"
tags: ["linux","RedesComunitarias","libremesh","lokal"]
---

## Lokal 

As part of the [lokal projetct](https://wakoma.co/lokal/) the tests with two routers the Archer A7 V5.8 and Unifi Mesh UAP-AC-M are described below


libremesh firmwares -> https://next.coolab.org/s/Eiz7r9xJKiXi8MA

### Unifi Mesh UAP-AC-M

Unifi datasheet -> http://dl.ubnt.com/datasheets/unifi/UniFi_AC_Mesh_DS.pdf	

Follow this steps -> https://openwrt.org/toh/ubiquiti/unifiac?s[]=unifi&s[]=mesh#non-invasive_method_using_mtd

Breif

We're going to downgrade to older ubiquiti firmware version (ubnt.bin), install OpenWRT firmware, then install Libremesh firmware.


1. Download ubnt.bin from the folder

- md5sum BZ*.bin should return: 5bb23b387defcbd1f6cda5819c7905e5
- mv BZ*.bin ubnt.bin

2. static IP (192.168.1.0/24, do not use IP 192.168.1.20 or 192.168.1.1 for the computer, if unsure use IP 192.168.1.10, netmask 255.255.255.0, default gateway 192.168.1.1 for your PC)

3. Copy the Unifi-Firmware from your Linux-PC to the Unifi-device: scp ubnt.bin ubnt@192.168.1.20:/tmp/ (password is also ubnt)

4. SSH into the Unifi-device ssh ubnt@192.168.1.20 (password is also ubnt)

5. At your Unifi-device issue the command fwupdate.real -m /tmp/ubnt.bin. Let the Unifi-device reboot. 

6. scp the OpenWrt-Firmware to the Unifi-device scp openwrt-ath79-generic-ubnt_unifiac-XXX-squashfs-sysupgrade.bin ubnt@192.168.1.20:/tmp/

7.  SSH into the Unifi-device and: `mtd write /tmp/openwrt-xxxxx-squashfs-sysupgrade.bin kernel0`, afterwards also erase the now unused partition `mtd erase kernel1`

8. Find out which partition is named “bs”: cat /proc/mtd, expected result is “mtd4”. Then issue this command in the Unifi-device (use the obtained partition name for bs): dd if=/dev/zero bs=1 count=1 of=/dev/mtd4

9. On next reboot you will see an openwrt firmware.

    change static IP back to DHCP. Unplug and replug eth cable.

    


10. In openwrt go to upload firmware and upload the Libremesh firmware

    go to browser. 192.168.1.1
    username: root
    pass: empty

    System>> Back/Flash Firmware

    Flash Image
    Browse to libremesh squash
    Upload

    Leave all 3 boxes unchecked 
    click continue
    
    After flash go to thisnode.info
    
    
11. Create New Network

Choose a name: lokal.network
PW: Phubert pw

name for node uap-ac-mesh


    

### Archer A7 V5.8


1. Connect the lan cable in PC to router LAN-1 port
2. Open a browser and open the TP-Link default address http://192.168.0.1
You will be asked to create a password on first opening. Set a new password and login.
3. You should see the router access page. Select: Advanced/System-Tools/Firmware-Upgrade
5. Select: Manual-Upgrade/Browse: Select the file downloaded from “Firmware OpenWrt Install” section openwrt-22.03.5-ath79-generic-tplink_archer-a7-v5-squashfs-factory.bin
6. Wait until firmware flashing is done. Do not interrupt the process - risk of bricking the router!
7. After flashing is done you will see “page not found”. This is normal.
8. Unplug and replug eth cable, and open in browser the OpenWRT default address: http://192.168.1.1 (manual LAN-card settings: ip4:192.168.1.122/mask:255.255.255.0/gateway:192.168.1.1 )
9. From openwrt upograde with libremesh


    System >> Backup/Flash Firmware
    Flash Image
    Browse to librerouteros squashfs-sysupgrade.bin
    Upload

    Leave all 3 boxes unchecked 
    click continue
    


### Archer C7 V5


1. Connect the lan cable in PC to router LAN-1 port
2. Open a browser and open the TP-Link default address http://192.168.0.1
You will be asked to create a password on first opening. Set a new password and login.
3. You should see the router access page. Select: Advanced/System-Tools/Firmware-Upgrade
5. Select: Manual-Upgrade/Browse: Select the file downloaded from “Firmware OpenWrt Install” section openwrt-22.03.5-ath79-generic-tplink_archer-a7-v5-squashfs-factory.bin (use C7 version of this file)
6. Wait until firmware flashing is done. Do not interrupt the process - risk of bricking the router!
7. After flashing is done you will see “page not found”. This is normal.
8. Unplug and replug eth cable, and open in browser the OpenWRT default address: http://192.168.1.1 (manual LAN-card settings: ip4:192.168.1.122/mask:255.255.255.0/gateway:192.168.1.1 )
9. From openwrt upograde with libremesh
    System >> Backup/Flash Firmware

    Flash Image
    Browse to librerouteros squashfs-sysupgrade.bin
    Upload

    Leave all 3 boxes unchecked 
    click continue



### Ansible install

python3 -m venv venv
source venv/bin/activate
pip install ansible
ansible-playbook -i hosts/preparar prepare.yml 
ansible-playbook -i hosts/nucserver.yml playbook.yml 


### Certificates

Some discutions aboute that - https://communitynetworks.group/t/anyone-using-https-in-a-cn/286/26

The method used - https://geekrewind.com/generate-free-wildcard-certificates-using-lets-encrypt-certbot-on-ubuntu-18-04/

```sudo certbot certonly --manual --preferred-challenges=dns --email hiure@riseup.net --server https://acme-v02.api.letsencrypt.org/directory --agree-tos -d redepsp.info -d *.redepsp.info```

Add txt records according to the certbot instructions

```sudo certbot certificates```

```mv fullchain.pem redepsp.info.crt```

```openssl pkey -in privkey.pem -out redepsp.info.key```

Copy certificates to ansible host folder 

`cp redepsp.info* hosts/ `

### Ansible config

Instructions - https://docs.lokal.network/gettingstarted/

Clone the repository - git clone https://github.com/Wakoma/Lokal.git

`rm ansible.cfg` 

`ansible-galaxy install -r requirements.yml`

hosts/preparar

```
all:
  hosts: "10.208.191.255"
  vars:
    app_user: psp
    ansible_user: root
    setup_ssh: true
    ssh_key: ssh-rsa 
```

`ansible-playbook -i hosts/preparar prepare.yml`

hosts/nucserver

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

`ansible-playbook -i hosts/nucserver.yml playbook.yml`

#### Adding subdomain to wordpress

in the file `roles/wordpress/defaults/main.yml`

add the subdomain:

```subdomain_wordpress: lokal```

### Dnsmasq config

Edit the file `/etc/config/lime-community` and add your domain

```
config lime 'system'
	option domain 'redepsp.info'

config lime 'network'

config lime 'wifi'
	option ap_ssid 'PSP'
	option apname_ssid 'PSP/%H'
```

Apply changes: 

`lime-config` 

If no erros return use:

`lime-apply`

Edit the dnsmasq file `/etc/dnsmasq.d/lokal.conf`

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

Edit the pirania file under `/etc/config/pirania` 

 - to add the destination page to redirect to, change the `option portal_domain` line to your domain and the `option url_portal` line to `/` 
 - to catch all clients, change the `list catch_interfaces`
 - to change the portal open time `option duration_m`.

My example

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

After that do `captive portal stop` and `captive-portal start`


## Misc

I had a problem with traefik and transmission's password so I had to install this

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



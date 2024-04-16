---
title: "Como Usar o Ubus no Libremesh"
date: 2021-02-14
description: "Com o pacote de ferramentas Ubus você pode mexer em tudo que é configuração no seu libremesh."
image: "/images/terminal.png"
type: "post"
tags: ["RedesComunitarias","libremesh"]
---


### Tutorial: Introdução ao Ubus no Libremesh para Iniciantes

#### Passo 1: O que é Ubus e Libremesh
O Ubus é uma ferramenta poderosa para gerenciar redes mesh baseadas em OpenWrt, como o Libremesh. Ele facilita a comunicação entre processos do sistema, fornecendo uma base completa de informações. Saiba mais sobre o [Ubus](https://openwrt.org/docs/techref/ubus) e o [Libremesh](https://libremesh.org).
Como o Ubus é um programa instalado dentro do roteador você precisa acessar o terminal do roteador [Veja como fazer isso aqui](/posts/Como-ascessar-roteador-por-ssh)

#### Passo 2: Comandos Básicos do Ubus
Para começar, você pode usar o comando `ubus list`  para listar os objetos disponíveis e `ubus call` para chamar um serviço específico. Veja a sintaxe simples de uso do Ubus:

```
root@conteiner:~# ubus
Usage: ubus [<options>] <command> [arguments...]
Options:
 -s <socket>:		Set the unix domain socket to connect to
 -t <timeout>:		Set the timeout (in seconds) for a command to complete
 -S:			Use simplified output (for scripts)
 -v:			More verbose output
 -m <type>:		(for monitor): include a specific message type
			(can be used more than once)
 -M <r|t>		(for monitor): only capture received or transmitted traffic

Commands:
 - list [<path>]			List objects
 - call <path> <method> [<message>]	Call an object method
 - listen [<path>...]			Listen for events
 - send <type> [<message>]		Send an event
 - wait_for <object> [<object>...]	Wait for multiple objects to appear on ubus
 - monitor				Monitor ubus traffic
```

#### Passo 3: Explorando Serviços do Ubus
Ao usar `ubus list`, você pode ver os serviços disponíveis, como os relacionados ao Lime-utils, que oferecem funcionalidades úteis para o Libremesh. Por exemplo, ao chamar `ubus -v list lime-utils`, você pode ver os métodos disponíveis:

```
root@conteiner:~# ubus list
dnsmasq
hostapd.wlan0-ap
hostapd.wlan0-apname
lime-batman-adv
lime-fbw
lime-groundrouting
lime-location
lime-metrics
lime-openairview
lime-utils
log
network
network.device
network.interface
network.interface.lan
network.interface.lm_net_batadv_dummy_if
network.interface.lm_net_br_lan_anygw_if
network.interface.lm_net_eth0_1_babeld_if
network.interface.lm_net_eth0_babeld_if
network.interface.lm_net_eth1_babeld_if
network.interface.lm_net_eth1_batadv_if
network.interface.lm_net_wlan0_mesh
network.interface.lm_net_wlan0_mesh_babeld_if
network.interface.lm_net_wlan0_mesh_batadv_if
network.interface.lm_net_wlan1_mesh
network.interface.lm_net_wlan1_mesh_babeld_if
network.interface.lm_net_wlan1_mesh_batadv_if
network.interface.loopback
network.interface.wan
network.interface.wan6
network.rrdns
network.wireless
pirania
pirania-app
service
session
system
uci
```

#### Passo 4: Chamando Serviços com Ubus
Vamos chamar o serviço `lime-utils` usando o comando `ubus call lime-utils get_cloud_nodes` para obter uma lista de nós na rede mesh:

```
root@conteiner:~# ubus call lime-utils get_cloud_nodes
{
	"nodes": [
		"alessandra",
		"anapaula",
		"arcanjo",
		...
	],
	"status": "ok"
}
```

#### Passo 5: Interpretação dos Resultados
Ao chamar o serviço, você receberá uma lista de nós na rede mesh, como "alessandra", "anapaula", etc. Essas informações podem ser úteis para monitorar e gerenciar sua rede.

#### Passo 6: Dicas Adicionais
Explore mais serviços do Ubus, experimente diferentes comandos e lembre-se de consultar a documentação para aprender mais sobre suas capacidades.

#### Passo 7: Exercícios Práticos
Pratique chamando outros serviços, modificando parâmetros e explorando mais recursos do Ubus para aprofundar seu conhecimento e habilidades.

Com esses passos, você estará mais preparado para utilizar o Ubus no Libremesh e aproveitar ao máximo suas funcionalidades para gerenciar sua rede mesh de forma eficiente.

Uma das maneiras mais poderosas de encontrar informações na sua rede mesh baseada em openwrt é utilizando o [Ubus](https://openwrt.org/docs/techref/ubus). Ele fornece uma [comunicação entre processos](https://pt.wikipedia.org/wiki/Comunica%C3%A7%C3%A3o_entre_processos) do sistema reunindo assim uma base bem completa de informação. Como ele você pode consultar sobre os processos e caracteristicas do seu sistema como também modificalos.




---
title: "How to Use Ubus in Libremesh"
date: 2021-02-14
description: "With the Ubus tool package, you can tweak all configurations in your Libremesh."
image: "/images/terminal.png"
type: "post"
tags: ["CommunityNetworks","libremesh"]
---


### Introduction to Ubus in Libremesh for Beginners

#### Step 1: What is Ubus and Libremesh
Ubus is a powerful tool for managing mesh networks based on OpenWrt, such as Libremesh. It facilitates communication between system processes, providing a comprehensive information base. Learn more about [Ubus](https://openwrt.org/docs/techref/ubus) and [Libremesh](https://libremesh.org).
Since Ubus is a program installed within the router, you need to access the router's terminal [See how to do it here](/posts/How-to-access-router-via-ssh)

#### Step 2: Basic Ubus Commands
To get started, you can use the `ubus list` command to list available objects and `ubus call` to invoke a specific service. Here is the simple syntax for using Ubus:

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
#### Step 3: Exploring Ubus Services
By using `ubus list`, you can see the available services, such as those related to Lime-utils, which offer useful functionalities for Libremesh. For example, by calling `ubus -v list lime-utils`, you can see the available methods:

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
#### Step 4: Calling Services with Ubus
Let's call the `lime-utils` service using the command `ubus call lime-utils get_cloud_nodes` to obtain a list of nodes in the mesh network:

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

#### Step 5: Interpreting the Results
When calling the service, you will receive a list of nodes in the mesh network, such as "alessandra," "anapaula," etc. This information can be useful for monitoring and managing your network.

#### Step 6: Additional Tips
Explore more Ubus services, try different commands, and remember to consult the documentation to learn more about its capabilities.

#### Step 7: Practical Exercises
Practice calling other services, modifying parameters, and exploring more Ubus resources to deepen your knowledge and skills.

With these steps, you will be better prepared to use Ubus in Libremesh and make the most of its features to efficiently manage your mesh network.

One of the most powerful ways to find information in your openwrt-based mesh network is by using [Ubus](https://openwrt.org/docs/techref/ubus). It provides a [communication between processes](https://en.wikipedia.org/wiki/Inter-process_communication) of the system, thus gathering a very comprehensive base of information. With it, you can inquire about the processes and characteristics of your system as well as modify them.


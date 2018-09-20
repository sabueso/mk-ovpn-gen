# Mk-ovpn-gen

Mk-ovpn-gen is a role oriented to generate files to configure Openvpn on Mikrotik + clients, as easy as run a playbook providing the correct credentials of the Mikrotik router.

This playbook don't use the easy-rsa package and do all the work using the internal tools of Mikrotik devices.

### Requirements

	- Ansible 2.7
	- Openvpn 2.3 (tested on Debian 8/9)


### Configuration

We use paramiko in order to comunicate correctly with Mikrotik devices.
Edit your ansible.cfg adding this part of code:

```sh
[paramiko_connection]
pty=False
look_for_key=no
```

### Usage

Use the main playbook file, or integrate the role in your playbook, as you wish.

```sh
$ ./mkvpn.yml -i 192.168.88.1, -u admin --ask-pass

```

## Config file for client

```sh
dev tun
proto tcp-client
remote <ip_address_of_your_router> 1194

ca      ca.crt
cert    client1.crt
key     client1.key
askpass	client1.pass

tls-client

user nobody
group nogroup

# More reliable detection when a system loses its connection.
ping 15
ping-restart 45
ping-timer-rem
persist-tun
persist-key

mute-replay-warnings

verb 3

cipher AES-256-CBC
auth SHA1
pull

auth-user-pass user.cfg
```

This file should be generated by some role included with this repo

### Todos

- Validate openvpn is installed
- Download certs to client
- Rename to clear name downloaded files
- Generate CFG config with correct files
- Create auth.cfg & client1.pass
- Edit /etc/default/openvpn for Debian users
- Restart openvpn to force connect

License
----

MIT


**Free Software, Hell Yeah!**

----
Ramiro <ramiro_at_gnubit_dot_com>

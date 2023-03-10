
Pure Layer 2 OpenVPN config with DHCP from the LAN

As root :

* Install OpenVPN and Easy-RSA

```apt install openvpn easy-rsa```

* We need to modify the systemctl startup script
Update /usr/lib/systemd/system/openvpn-server@.service

```
Add or update under [Service]
WorkingDirectory=/etc/openvpn/server
ExecStartPre=/etc/openvpn/server/scripts/bridge-start
LimitNPROC=100
```

Don't forget to put the script there :

```
mkdir -p /etc/openvpn/server/scripts
wget https://raw.githubusercontent.com/philippebourcier/openvpn_confs/main/bridge-start
chmod 755 bridge-start
```

* Getting things ready for first launch
Update /etc/default/openvpn with

```AUTOSTART="server"```

Enable openvpn at startup :

```
cd /etc/openvpn/server
wget https://raw.githubusercontent.com/philippebourcier/openvpn_confs/main/server.conf
vi server.conf # edit the params that needs to be changed...
systemctl enable openvpn-server@server.service
systemctl enable openvpn
```

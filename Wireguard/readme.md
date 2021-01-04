# Wireguard configuration

## Why Wireguard?

## Network scheme

Server VPN:
- Xiaomi MI9
- 4G+
- VPN IP: 172.16.1.1/32

Client VPN:
- Ubuntu Server 20.04 LTS
- ADSL2+
- VPN IP: 172.16.1.2/32

## Client configuration

### Download the Wireguard client application
https://play.google.com/store/apps/details?id=com.wireguard.android&hl=fr&gl=US

### 

## Server configuration

### Install Wireguard

```python
sudo apt install wireguard
```

### Configuring a new public/private key
```python
umask 077

# Create a new private key
wg genkey > privatekey

# Create a new public key from the private key
wg pubkey < privatekey > publickey
```

### Configuring a new wireguard tunnel interface

This Wireguard tunnel interface will be call "wg0". You can use whatever name you want, but keep in mind to be consistent.

```python
# Create a new tunnel interface
sudo ip link add dev wg0 type wireguard

# Assign an IP address to it
sudo ip address add dev wg0 YOUR_SERVER_VPN_IP

# Bind your tunnel interface to your client
sudo wg set wg0 peer YOUR_CLIENT_PUBLIC_KEY allowed-ips YOUR_CLIENT_VPN_IP
```




### Conf
```python
ip link add wg0 type wireguard
ip addr add 10.0.0.1/24 dev wg0
wg set wg0 private-key /etc/wireguard/server/server.key
wg set wg0 listen-port 51820
ip link set wg0 up
wg set wg0 peer Z0fOtR8quXMu2mPGsRAciAZFJ1XTXYWN5IkshaqXajo= allowed-ips 10.0.0.2/32 endpoint 192.168.1.38:51820
```

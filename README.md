

# ArvanCloud No Filter VPN

### ⚠ Attention ⚠
#### 1. This repository scanned with VirusTotal: [view result](https://www.virustotal.com/gui/url/04b321f9d729e438340b1d4c0b6c7f1a2fad57f6d6e4fea6c83af9803e524a1f)
#### 2. If see `Fail to detect internet connection: Unable to resolve host "cp.cloudflare.com".No address associated w.."` when client connect to server check this link [issue link](https://github.com/amircloner/tcp-vpn-proxy/issues/1)

## 0.Requirements

 1. Valid Domain Name Recommended **.ir**
 2. [ArvanCloud](https://arvancloud.com) Account
 3. PaaS Or Any Debian Servers the help of DockerFile
 4. Minimum Server Requirements (**RAM:** 256 MB, **CPU:** 0.5, **Disk:** 10G **Location:** out of IRAN)
 5. Random Password ([Online UUID Generator](https://www.uuidgenerator.net/))

## 1. Server Configuration

### 1.1 Install Docker

```console
curl -sSL https://gist.github.com/amircloner/4305b461df40616a1c4c432b3619af82/raw | bash
```
### 1.2 Clone Github Project
```console
git clone https://github.com/amircloner/tcp-vpn-proxy.git && cd tcp-vpn-proxy
```

### 1.3 Build Dockerfile

```console
 docker build -t amircloner/tcp-vpn-proxy:v1.0.0 .
```
### 1.4 Run Docker Image
 
The docker environment variables required are:

```txt

Domain : The domain of your server without the schema(https, http etc). Ex: test.com, not https://test.com

Password : Password you want to set for the Shadowsocks VPN service. EX: 0734e365-ac11-43b0-97d0-7923477e6dd5

PORT : Server port. Ex: 80

```
```console
 docker run -d --restart=always -p {PORT}:{PORT} --env Domain={Domain} --env Password={Password} --env PORT={PORT} amircloner/tcp-vpn-proxy:v1.0.0
 ```
  
### 1.5 Connect Server to ArvanCloud CDN
	

 1. Login into ArvanCloud Account
 2. In CDN
 3. Click  + Add new domains
 4. Add new Domain
 5. In CDN > DNS Records
 6. Create new Records (Subdomain) that equal to {Domain} point to server IP
 7. Check Arvan CDN is Enable
 8. Origin server connection protocol > HTTP
 9. Set {PORT} and Server IP

### 1.6 Verification Server


After the server is deployed, open app to display the webpage normally. After the address is filled with the path (for example: <https://{Domain}/static>), the 404 page is displayed, which means the deployment is successful.


## 2. Client Configuration

  

### QR code address:

```

https://{Domain}/qr

```

  

(Change {Domain} to your own app server url.)

  

Use the client (Shadowsocks recommended) to scan the QR code.

  

**or**

  

### Use 'ss' address:

```

https://{Domain}/ss

```

(Change {Domain} to your own app server url.)

  

Copy the details after opening and import it to the client.

  

**or**

  

### Manual configuration (Config file):

  

```json

{

"server" : "{Domain}",

"server_port" : 443,

"local_port" : 1080,

"password":"{password}",

"timeout":300,

"method":"chacha20-ietf-poly1305",

"mode": "tcp_only",

"fast_open":false,

"reuse_port":true,

"no_delay":true,

"plugin": "v2ray-plugin",

"plugin_opts":"path=/v2;host={Domain};tls",

"remarks" : "Private VPN"

}

```

Change {Domain} with your server url and {password} with your password.

  
## 3. Clients

  

### Android

  

[shadowsocks](https://play.google.com/store/apps/details?id=com.github.shadowsocks&hl=en_IN&gl=US)

  

[v2ray-plugin](https://play.google.com/store/apps/details?id=com.github.shadowsocks.plugin.v2ray)

  

### Windows

  

[ShadowSocks-Windows](https://github.com/shadowsocks/shadowsocks-windows/releases/download/4.4.1.0/Shadowsocks-4.4.1.0.zip)

  

[V2-Ray Plugin](https://github.com/shadowsocks/v2ray-plugin/releases/download/v1.3.1/v2ray-plugin-windows-amd64-v1.3.1.tar.gz)

  

Extract and keep v2ray plugin in the same folder as shadowsocks.

  

### Linux

  

[shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev)

  

[V2-Ray Plugin](https://github.com/shadowsocks/v2ray-plugin/releases/download/v1.3.1/v2ray-plugin-linux-amd64-v1.3.1.tar.gz)

  

Install the shadowsocks library, download and move the v2ray plugin in '/usr/bin' and use the following command to connect to VPN:

```

ss-local -c "config file location on your system"

```

Then use any proxy script to route your system's requests through your VPN.

Ex:

- [Proxy SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif?hl=en) : This extension can be used in chrome

- Polipo : Routes all of the network through your proxy

  

### Reference Guide for client setup

[Guide](https://zhaorengui.github.io/network/software/2018/08/10/shadowsocks-switchyOmega-en/)

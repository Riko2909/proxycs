
# Proxy Cheat Sheet for some Services with credentials

> **Note**
Some of these settings aren't tested yet. Please give some Feedback under **ISSUES**. 

**Usage (*example*)**

| [username]  | [Password]  | [IP]  | [Port]  |
|---|---|---|---|
| jerry  | PassWord123  | 172.56.230.11  | 3128  |

## Windows
### WinHTTP Proxy
To show the current proxy configuration, type `netsh winhttp show proxy` in your console.

To change these settings, use:
`netsh winhttp set proxy "[IP]:[Port]" bypass-list="172.*,example.com,<local>"`

## Linux
### Apt Proxy
First edit/create an configfile with `nano /etc/apt/apt.conf.d/proxy.conf` and add:
```
Acquire {
  HTTP::proxy "http://[username]:[Password]@[IP]:[Port]/";
  HTTPS::proxy "http://[username]:[Password]@[IP]:[Port]/";
}
```
### Enviroment for current shell and **all processes** started from current shell 
```
export http_proxy=http://[username]:[Password]@[IP]:[Port]/
export https_proxy=http://[username]:[Password]@[IP]:[Port]/
```
### Enviroment permanently and system wide

Edit the enviroment file with `nano /etc/environment` and add:
```
HTTP_PROXY="http://[username]:[Password]@[IP]:[Port]/"
HTTPS_PROXY="http://[username]:[Password]@[IP]:[Port]/"
```
## NodeJS (NPM)
```
npm config set proxy http://[username]:[Password]@[IP]:[Port]/
npm config set https-proxy http://[username]:[Password]@[IP]:[Port]/
```
## Yarn
```
yarn config set proxy http://[username]:[Password]@[IP]:[Port]/
yarn config set https-proxy http://[username]:[Password]@[IP]:[Port]/
```
## Git
```
git config --global http.proxy http://[username]:[Password]@[IP]:[Port]/
git config --global https.proxy http://[username]:[Password]@[IP]:[Port]/
```
## Maven
Edit the `proxies` session in your `~/.m2/settings.xml`
```
<proxies>
    <proxy>
        <id>id</id>
        <active>true</active>
        <protocol>[http]</protocol>
        <username>[username]</username>
        <password>[password]</password>
        <host>[host]</host>
        <port>[port]</port>
        <nonProxyHosts>example.com</nonProxyHosts>
    </proxy>
</proxies>
```
## Docker
Create a systemd drop-in directory for the `docker` service:

-   ``` sudo mkdir -p /etc/systemd/system/docker.service.d ```
    
-   Create/Edit a file with `nano /etc/systemd/system/docker.service.d/http-proxy.conf` that adds the environment variables:
```
[Service]
Environment="HTTP_PROXY=http://[username]:[Password]@[IP]:[Port]/"
Environment="HTTPS_PROXY=http://[username]:[Password]@[IP]:[Port]/"
Environment="NO_PROXY=localhost,127.0.0.1"
```
Flush changes and restart Docker

```
sudo systemctl daemon-reload
sudo systemctl restart docker
```
## Gradle
Edit the file `gradle.properties` and add:

**HTTP-Proxy**
```
systemProp.http.proxyHost=[IP]
systemProp.http.proxyPort=[Port]
systemProp.http.proxyUser=[username]
systemProp.http.proxyPassword=[Password]
systemProp.http.nonProxyHosts=localhost|127.0.0.1
```
**HTTPS-Proxy**
```
systemProp.https.proxyHost=[IP]
systemProp.https.proxyPort=[Port]
systemProp.https.proxyUser=[username]
systemProp.https.proxyPassword=[Password]
systemProp.https.nonProxyHosts=localhost|127.0.0.1
```

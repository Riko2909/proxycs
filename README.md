
# Proxy Cheat Sheet for some Services with credentials

## Linux
### Enviroment for current shell and **all processes** started from current shell 

    export http_proxy=http://[username]:[Password]@[IP]:[Port]/
    export https_proxy=http://[username]:[Password]@[IP]:[Port]/

### Enviroment permanently and system wide

 1. Open `nano /etc/environment`
 2. Append the following to the file

        HTTP_PROXY="http://[username]:[Password]@[IP]:[Port]/"
        HTTPS_PROXY="http://[username]:[Password]@[IP]:[Port]/"



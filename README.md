# Jupyter_Server
A guide on configuring a HTTPS, DNS hosted, Jupyter Lab server.

## Install Jupter Lab

### 1. Install Jupyter Lab

```{bash}
sudo apt update
sudo apt-get update
sudo apt install python3-pip
sudo apt install jupyter
pip3 install jupyterlab
export PATH="$HOME/.local/bin:$PATH"
```

### 2. Generate a configuration file and set a password

```{bash}
jupyter lab --generate-config
jupyter lab password
```
### 3. Confirm password is encrypted (hashed)

```{bash}
nano $HOME/.jupyter/jupyter_server_config.json
```

### 4. Configure Jupter Lab for DNS hosting

```{json}
{  
  "NotebookApp": {
    "password": "YOUR ENCRYPTED PASSWORD IS HERE",
    "allow_remote_access":true,
    "ip":"*",
    "port":8888,
    "allow_root":true
  }
}
```

## Setup DuckDNS

## Setup Nginx

### Install Nginx

#### Create a `.conf` in the directory, `/etc/nginx/sites-available`.

```
sudo nano /etc/nginx/sites-available/rename.duckdns.org.conf
```

#### Added the following lines into the created `.conf` file. Change `rename.duckdns.org` to your DuckDNS server name. 

```
server {
    listen 80;  # Listen on HTTP (port 80)
    server_name rename.duckdns.org;

    return 301 https://$server_name$request_uri;  # Redirect to HTTPS
}

server {
    listen 443 ssl; # Listen on port 443 for HTTPS
    server_name rename.duckdns.org;

    ssl_certificate /etc/letsencrypt/live/yourname.duckdns.org/fullchain.pem; 
    ssl_certificate_key /etc/letsencrypt/live/yourname.duckdns.org/privkey.pem;

    location / {
        proxy_pass http://127.0.0.1:8888; # Replace 8888 with Jupyter's actual port
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```























## Sources:
Medium Article: [Set up Remote Jupyter Lab/Notebook Server for Browser Access](https://medium.com/@mlquest0/set-up-remote-jupyter-lab-notebook-server-for-remote-browser-access-2cef464f203e)

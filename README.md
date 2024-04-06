# Jupyter_Server
A guide on configuring a HTTPS, DNS hosted, Jupyter Lab server.

## Install Jupter Lab

### 1. Update and upgrade system

```{bash}
sudo apt update
sudo apt upgrade
sudo apt-get update
sudo apt-get upgrade
```

### 2. Install Jupyter Lab

```{bash}
pip3 install jupyterlab
```

### 3. Generate a configuration file and set a password

```{bash}
jupyter lab --generate-config
jupyter lab password
```
### 4. Confirm password is encrypted (hashed)

```{bash}
nano /home/ubuntu/.jupyter/jupyter_server_config.json
```

### 5. Configure Jupter Lab for DNS hosting

```{json}
{  
  "NotebookApp": {
    "password": "YOUR ENCRYPTED PASSWORD IS HERE",
    "allow_remote_access":true,
    "ip":"*",
    "port":80,
    "allow_root":true
  }
}
```

## Setup DuckDNS

























## Sources:
Medium Article: [Set up Remote Jupyter Lab/Notebook Server for Browser Access](https://medium.com/@mlquest0/set-up-remote-jupyter-lab-notebook-server-for-remote-browser-access-2cef464f203e)

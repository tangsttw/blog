---
title: "Connect to Jupyter Notebook on Remote Server"
date: 2018-04-09T14:57:53+08:00
draft: false
description: ""
tags: [jupyter notebook]
categories: [jupyter notebook]
author: "YT"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
mathjax: true
---

If you installed jupyter notebook on a server and would like to access the jupyter notebook application from another computer, there are several steps need to be done. Follow the instructions below, then you can access the browser-based jupyter notebook from your computer.


# Step 1 - Generate configuration file
The first thing to be done is to generate a configuration file. In this file, we can configure the password used to login and access jupyter notebook from remote, and also configure the port at which will jupyter notebook be launched.
```
$ jupyter notebook --generate-config
```
By this instruction will generate a configuration file named `jupyter_notebook_config.json` under `~/.jupyter/` directory.


# Step 2 - Set login password
In this step we are going to setup a password for authenticating the login instead of using a token. This passord is set for login from remote computer.
```
$ jupyter notebook password
Enter password:  ****
Verify password: ****
\[NotebookPasswordApp\] Wrote hashed password to /Users/you/.jupyter/jupyter\_notebook\_config.json

```
This instruction performs a setup process with password defined by user input. Then, it will hash the password and store it in configuration file.

# Step 3 - Set launch configuration
This is the key step for setting up remote access to jupyter notebook. Generally, there are two ways to perform this step, (1) through ssh and (2) launch a public server.

## 1. through ssh
This is a relatively simple way thant the other. The only thing need to be done on server side is launch jupyter notebook on a certain port.
```
$ jupyter notebook --no-browser --port=[user-define-port]

ex.
jupyter notebook --no-browser --port=8889
```
The `--no-browser` option will launch jupyter notebook without opening a browser on local server.
Next step is to connect from remote computer with ssh.

## 2. launch a public server (skip step 4)
In this way, we will launch jupyter notebook on a public port using web server. Therefore, we have to setup SSL for web certificate first.
We use openssl to generate self-signed certificate.
```
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout [/path/to/store/mykey.key] -out [/path/to/store/mykeymycert.pem]
$ jupyter notebook --certfile=mycert.pem --keyfile mykey.key
```
After this, we setup the jupyter notebook configuration file. Open and edit the file `jupyter_notebook_config.py` under `~/.jupyter/` directory. In the configuration file, setting commands are commented by default. To enable the setting, uncomment and edit the code with our information.
```shell
# Set options for certfile, ip, password, and toggle off
# browser auto-opening
c.NotebookApp.certfile = u'[/absolute/path/to/your/certificate/mycert.pem]'
c.NotebookApp.keyfile = u'[/absolute/path/to/your/certificate/mykey.key]'
# Set ip to '*' to bind on all interfaces (ips) for the public server
c.NotebookApp.ip = '*'
# The password is generated from step 2
c.NotebookApp.password = u'sha1:bcd259ccf...<your hashed password here>'
#
c.NotebookApp.open_browser = False

# It is a good idea to set a known, fixed port for server access
c.NotebookApp.port = [user-define-port]
```
After the configuration, we can now connect to [ip]:[user-define-port] from remote computer to access jupyter notebook.

# Step 4 - Client side setting
If you choose to setup jupyter notebook server through ssh in [step 3](#1-through-ssh), there are little setup should be done on client side.
Use ssh to connect to server via the port where jupyter notebook is launched and bind it to localhost 8888 port.
```
ssh -N -L localhost:8888:localhost:[server-port] [user]@[remote-server]
```
Then, open `localhost:8888` in browser to access jupyter notebook.
```
localhost:8888
```


### Reference
http://jupyter-notebook.readthedocs.io/en/stable/public_server.html

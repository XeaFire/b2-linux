# LE TP 1

## 3. sudo c pa bo

### 🌞 Ajouter votre utilisateur au groupe docker

```bash
[tristan@docker ~]$ sudo usermod -aG docker tristan

[tristan@docker ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
 ```

## 4. Un premier conteneur en vif

### 🌞 Lancer un conteneur NGINX

```bash
[tristan@docker ~]$ 🌞 Lancer un conteneur NGINX
-bash: 🌞: command not found
[tristan@docker ~]$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete
650ee30bbe5e: Pull complete
8cc1569e58f5: Pull complete
362f35df001b: Pull complete
13e320bf29cd: Pull complete
7b50399908e1: Pull complete
57b64962dd94: Pull complete
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
8d3777994d34d32c41b2899259631f3ee562048be440730a4927c730e7b1e02b
```

```bash 
[tristan@docker ~]$ dk ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS
   NAMES
8d3777994d34   nginx     "/docker-entrypoint.…"   4 minutes ago   Up 4 minutes   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp



[tristan@docker ~]$ dk logs 8d
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/11 09:50:58 [notice] 1#1: using the "epoll" event method
2024/12/11 09:50:58 [notice] 1#1: nginx/1.27.3
2024/12/11 09:50:58 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/12/11 09:50:58 [notice] 1#1: OS: Linux 5.14.0-427.37.1.el9_4.x86_64
2024/12/11 09:50:58 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1073741816:1073741816
2024/12/11 09:50:58 [notice] 1#1: start worker processes
2024/12/11 09:50:58 [notice] 1#1: start worker process 29
10.1.1.1 - - [11/Dec/2024:09:53:17 +0000] "GET / HTTP/1.1" 200 615 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36" "-"
10.1.1.1 - - [11/Dec/2024:09:53:17 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://10.1.1.15:9999/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36" "-"
2024/12/11 09:53:17 [error] 29#29: *1 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 10.1.1.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "10.1.1.15:9999", referrer: "http://10.1.1.15:9999/"
```


```bash
[tristan@docker ~]$ dk inspect 8d
[
    {
        "Id": "8d3777994d34d32c41b2899259631f3ee562048be440730a4927c730e7b1e02b",
        "Created": "2024-12-11T09:50:55.636092Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            ...
```


```bash
[sudo] password for tristan:
State     Recv-Q    Send-Q       Local Address:Port       Peer Address:Port   Process
LISTEN    0         128                0.0.0.0:22              0.0.0.0:*       users:(("sshd",pid=688,fd=3))
LISTEN    0         4096               0.0.0.0:9999            0.0.0.0:*       users:(("docker-proxy",pid=1548,fd=4))
LISTEN    0         128                   [::]:22                 [::]:*       users:(("sshd",pid=688,fd=4))
LISTEN    0         4096                  [::]:9999               [::]:*       users:(("docker-proxy",pid=1553,fd=4))
```

j'ai cut c'était long

```bash
[tristan@docker ~]$ sudo firewall-cmd --add-port=9999/tcp --permanent
[sudo] password for tristan:
success 
```

```bash
PS C:\Users\trist> curl http://10.1.1.15:9999


StatusCode        : 200
StatusDescription : OK
Content           : <!DOCTYPE html>
                    <html>
                    <head>
                    <title>Welcome to nginx!</title>
                    <style>
                    html { color-scheme: light dark; }
                    body { width: 35em; margin: 0 auto;
                    font-family: Tahoma, Verdana, Arial, sans-serif; }
                    </style...
RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 615
                    Content-Type: text/html
                    Date: Wed, 11 Dec 2024 10:36:02 GMT
                    ETag: "6745ef54-267"
                    Last-Modified: Tue, 26 Nov 2024 ...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 615], [Content-Type,
                    text/html]...}
Images            : {}
InputFields       : {}
Links             : {@{innerHTML=nginx.org; innerText=nginx.org; outerHTML=<A href="http://nginx.org/">nginx.org</A>;
                    outerText=nginx.org; tagName=A; href=http://nginx.org/}, @{innerHTML=nginx.com;
                    innerText=nginx.com; outerHTML=<A href="http://nginx.com/">nginx.com</A>; outerText=nginx.com;
                    tagName=A; href=http://nginx.com/}}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 615
```

### 🌞 On va ajouter un site Web au conteneur NGINX


``` bash
[tristan@docker ~]$ docker run -d -p 9999:8080 -v /home/tristan/nginx/index.html:/var/www/html/index.html -v /home/tristan/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
2f881d256667550e1eb68d1df3e6917ccad1c4edbca574f52bfc7a0ff62b44a0
```

``` bash
PS C:\Users\trist> curl http://10.1.1.15:9999


StatusCode        : 200
StatusDescription : OK
Content           : <h1> Plop vends pano bouftou j'ai pas pano kwak donc j'en ai plus besoin enfin <h1>

RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 84
                    Content-Type: text/html
                    Date: Wed, 11 Dec 2024 10:46:14 GMT
                    ETag: "67596c82-54"
                    Last-Modified: Wed, 11 Dec 2024 10...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 84], [Content-Type,
                    text/html]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 84

```


``` bash
PS C:\Users\trist> curl http://10.1.1.15:9999


StatusCode        : 200
StatusDescription : OK
Content           : <h1> Plop vends pano bouftou j'ai pas pano kwak donc j'en ai plus besoin enfin <h1>

RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 84
                    Content-Type: text/html
                    Date: Wed, 11 Dec 2024 10:46:14 GMT
                    ETag: "67596c82-54"
                    Last-Modified: Wed, 11 Dec 2024 10...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 84], [Content-Type,
                    text/html]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 84

```

## 5. Un deuxième conteneur en vif


```bash
[tristan@docker ~]$ docker run -it python bash
Unable to find image 'python:latest' locally
latest: Pulling from library/python
fdf894e782a2: Pull complete
5bd71677db44: Pull complete
551df7f94f9c: Pull complete
ce82e98d553d: Pull complete
5f0e19c475d6: Pull complete
abab87fa45d0: Pull complete
2ac2596c631f: Pull complete
Digest: sha256:220d07595f288567bbf07883576f6591dad77d824dce74f0c73850e129fa1f46
Status: Downloaded newer image for python:latest
root@c3906ca1507c:/# pip install aiohttp aioconsole
Collecting aiohttp
  Downloading aiohttp-3.11.10-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
Collecting aioconsole
  Downloading aioconsole-0.8.1-py3-none-any.whl.metadata (46 kB)
Collecting aiohappyeyeballs>=2.3.0 (from aiohttp)
  Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl.metadata (6.1 kB)
Collecting aiosignal>=1.1.2 (from aiohttp)
  Downloading aiosignal-1.3.1-py3-none-any.whl.metadata (4.0 kB)
Collecting attrs>=17.3.0 (from aiohttp)
  Downloading attrs-24.2.0-py3-none-any.whl.metadata (11 kB)
Collecting frozenlist>=1.1.1 (from aiohttp)
  Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (13 kB)
Collecting multidict<7.0,>=4.5 (from aiohttp)
  Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.0 kB)
Collecting propcache>=0.2.0 (from aiohttp)
```

# II. Images

## 🌞 Récupérez des images  


```bash
docker pull mysql:5.7-oraclelinux7
```

# 2. Construire une image


# 🌞 Ecrire un Dockerfile pour une image qui héberge une application Python

```bash
[tristan@docker python_app_build]$ cat Dockerfile
FROM debian:bullseye-slim

RUN apt-get update && apt-get install -y python3 python3-pip

RUN pip3 install emoji

COPY app.py /app/app.py

ENTRYPOINT ["python3", "/app/app.py"]
```

# 🌞 Build l'image

```bash
docker build . -t python_app:version_de_ouf
```

```bash
[tristan@docker python_app_build]$ docker run ben
Cet exemple d'application est vraiment naze 👎
```

# 🌞 Créez un fichier docker-compose.yml

```bash
[tristan@docker compose]$ cat docker-compose.yml
version: "3"

services:
  conteneur_nul:
    image: debian
    entrypoint: sleep 9999
  conteneur_flopesque:
    image: debian
    entrypoint: sleep 9999
```

# 🌞 Lancez les deux conteneurs avec docker compose

```bash
[tristan@docker compose]$ docker compose up -d
WARN[0000] /home/tristan/compose/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 3/3
 ✔ conteneur_nul Pulled                                                                                           12.8s
   ✔ fdf894e782a2 Already exists                                                                                   0.0s
 ✔ conteneur_flopesque Pulled                                                                                     13.0s
[+] Running 3/3
 ✔ Network compose_default                  Created                                                                0.5s
 ✔ Container compose-conteneur_nul-1        Started                                                                1.4s
 ✔ Container compose-conteneur_flopesque-1  Started                                                                1.4s
```

# 🌞 Vérifier que les deux conteneurs tournent

```bash
[tristan@docker compose]$ docker ps
CONTAINER ID   IMAGE     COMMAND        CREATED          STATUS          PORTS     NAMES
3a628e91f20c   debian    "sleep 9999"   56 seconds ago   Up 55 seconds             compose-conteneur_nul-1
c51150a3b1cd   debian    "sleep 9999"   56 seconds ago   Up 55 seconds             compose-conteneur_flopesque-1
```

# 🌞 Pop un shell dans le conteneur conteneur_nul

```bash
[tristan@docker compose]$ docker exec -it 3a bash


root@3a628e91f20c:/# ping compose-conteneur_flopesque-1
PING compose-conteneur_flopesque-1 (172.18.0.2) 56(84) bytes of data.
64 bytes from compose-conteneur_flopesque-1.compose_default (172.18.0.2): icmp_seq=1 ttl=64 time=0.147 ms
64 bytes from compose-conteneur_flopesque-1.compose_default (172.18.0.2): icmp_seq=2 ttl=64 time=0.222 ms
64 bytes from compose-conteneur_flopesque-1.compose_default (172.18.0.2): icmp_seq=3 ttl=64 time=0.216 ms
^C
--- compose-conteneur_flopesque-1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2005ms
rtt min/avg/max/mdev = 0.147/0.195/0.222/0.034 ms
root@3a628e91f20c:/#
```
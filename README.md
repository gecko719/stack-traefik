### 1. 啟動services
~~~
# docker stack deploy -c docker-stack.yml t
Creating network t_traefik
Creating service t_traefik
Creating service t_whoami
Creating service t_nginx
~~~

### 2. 確認services己啟動
~~~
# docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE                      PORTS
kxgch2w0v3f8        t_nginx             replicated          0/1                 nginx:latest               
6is59wgcaism        t_traefik           replicated          1/1                 traefik:latest             *:80->80/tcp,*:443->443/tcp,*:8080->8080/tcp
uv0yd3cw8jpt        t_whoami            replicated          1/1                 emilevauge/whoami:latest   
~~~

### 3. 試著呼叫service

> host: dev.example.io

~~~
# curl --header "host: dev.example.io" http://10.0.1.7
Hostname: ec6389c53a3b
IP: 127.0.0.1
IP: 10.0.0.5
IP: 10.0.0.6
IP: 172.19.0.4
GET / HTTP/1.1
Host: dev.example.io
User-Agent: curl/7.35.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 10.255.0.2
X-Forwarded-Host: dev.example.io
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: 011bdf1e2c2c
X-Real-Ip: 10.255.0.2
~~~

> host: dev.example.nginx

~~~
# # curl --header "host: dev.example.nginx" http://10.0.1.7
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
~~~

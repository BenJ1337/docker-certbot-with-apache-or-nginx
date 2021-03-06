# Docker
## Apache as proxy to certbot

### Start the apache/httpd webserver
add Parameter -d after "up" to run the container as deamon in the brackground
#### Apache
```bash
$ docker-compose -f docker-compose.yml -f docker-compose.apache.yml up
or
$ bash runApache.sh
```

#### Nginx
```bash
$ docker-compose -f docker-compose.yml -f docker-compose.nginx.yml up
or 
$ bash runNginx.sh
```

### Activate proxy settings to forward requests to the Certbot standalone server configuration

uncommand the following line
```
Include conf/extra/httpd-conf/certbot-proxy/*.conf
```
in
```
./apache/httpd-conf/httpd-xtra.conf
```

to activate changes in the httpd configuration you need to reload the configuration

```bash
$ docker ps
$ docker exec -t <container-id> apachectl gracefull
```

### Run Docker Certbot
The scripts starts a Certbot container with a standalone server to execute the acme challenge
```bash
$ cd ./certbot/
$ bash request-cert.sh
```
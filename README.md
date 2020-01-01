### If you’re just getting started with nginx-proxy, start here. 

**
Clone this repository
**

```
git clone https://Majid-Rehman@bitbucket.org/Majid-Rehman/nginx-proxy.git
```
**
 Once that’s finished, issue the following command to create a unique network for nginx-proxy and other Docker containers to communicate through.
  **

```
docker network create nginx-proxy
```

**
Now, take a closer look at line 30, which contains - `./nginx.tmpl:/etc/docker-gen/templates/nginx.tmpl:ro.` This line creates a Docker volume between a file on your host filesystem (in this case, in the nginx-proxy directory) and a file inside one of the Docker containers. For that volume to work, we need to supply the nginx.tmpl file.
Inside of the nginx-proxy directory, use the following curl command to copy the developer’s sample `nginx.tmpl` file to your VPS. 
**

```
curl https://raw.githubusercontent.com/jwilder/nginx-proxy/master/nginx.tmpl > nginx.tmpl
```

**
You can now run the docker-compose command that will kick this all off.
**

```
docker-compose up -d
```

**
The process will start by downloading a few Docker images, and if things finish successfully, the output will end with the following:
**

```
Creating nginx-proxy ...
Creating nginx-proxy ... done
Creating nginx-proxy-gen ...
Creating nginx-proxy-gen ... done
Creating nginx-proxy-le ...
Creating nginx-proxy-le ... done
```

**
To confirm this, run `docker ps`. You should see three running containers, named `nginx-proxy`, `nginx-proxy-gen`, and `nginx-proxy-le`, like this:
**

```
CONTAINER ID        IMAGE                                    COMMAND                  CREATED             STATUS              PORTS                                      NAMES
9ea5fffc24dd        jrcs/letsencrypt-nginx-proxy-companion   "/bin/bash /app/en..."   4 minutes ago       Up 4 minutes                                                   nginx-proxy-le
e2288dfc3c5c        jwilder/docker-gen:0.7.3                 "/usr/local/bin/do..."   4 minutes ago       Up 3 seconds                                                   nginx-proxy-gen
eda8f12bd829        nginx:1.13.1                             "nginx -g 'daemon ..."   4 minutes ago       Up 4 minutes        0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx-proxy
```

** 
If any of those aren’t running, you should check their logs. You can do that with docker logs. 
**

```
$ docker logs nginx-proxy
$ docker logs nginx-proxy-gen
$ docker logs nginx-proxy-le
```

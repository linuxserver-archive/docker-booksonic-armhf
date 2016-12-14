[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/booksonic
[![](https://images.microbadger.com/badges/version/lsioarmhf/booksonic.svg)](https://microbadger.com/images/lsioarmhf/booksonic "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/booksonic.svg)](https://microbadger.com/images/lsioarmhf/booksonic "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/booksonic.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/booksonic.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-booksonic)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-booksonic/)
[hub]: https://hub.docker.com/r/lsioarmhf/booksonic/

[Booksonic][booksurl] is a server and an app for streaming your audiobooks to any pc or android phone. Most of the functionality is also availiable on other platforms that have apps for subsonic.

[![booksonic](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/booksonic.png)][booksurl]
[booksurl]: http://booksonic.org

## Usage

```
docker create \
  --name=booksonic \
-v </path/to/config>:/config \
-v </path/to/audiobooks>:/books \
-v </path/to/podcasts>:/podcasts \
-v </path/to/other media>:/media \
-e PGID=<gid> -e PUID=<uid> \
-e CONTEXT_PATH=<url-base> \
-e TZ=<timezone> \
-p 4040:4040 \
  lsioarmhf/booksonic
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 4040` - the port(s)
* `-v /config` - Configuration file location
* `-v /books` - Location of audiobooks.
* `-v /podcasts` - Location of podcasts.
* `-v /media` - Location of other media - *optional*
* `-e PGID` for for GroupID - see below for explanation - *optional*
* `-e PUID` for for UserID - see below for explanation - *optional*
* `-e CONTEXT_PATH` for setting url-base in reverse proxy setups - *optional*
* `-e TZ` for setting timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it booksonic /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Access WebUI at `<your-ip>:4040`.

Default user/pass is admin/admin

## Info

* Shell access whilst the container is running: `docker exec -it booksonic /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f booksonic`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' booksonic`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/booksonic`

## Versions

+ **13.12.16:** Initial Release.

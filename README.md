# arr-stack
## Full *arr Stack including VPNs, CIFS Storage, Monitoring, Media Server
you just have to specify the compose file in portainer as stack and add the following **environment variables**:
- USERNAME
- PASSWORD
- CIFS_USERNAME
- CIFS_PASSWORD

The Stack will require alot of ports, most of them are default to the docker image.
Due to the fact that it is not possible to set *network_mode: "service:vpn"* and add an additional network interface the traffic server had to be forced to use the host ports, so no clean port 80 only solution.

    - 8118:8118 # privoxy vpn1
    - 8119:8118 # privoxy vpn2
    - 8120:8118 # privoxy vpn3
    - 9091:9091 # transmission
    - 5299:5299 # lazylib
    - 9117:9117 # jackett
    - 8686:8686 # lidarr
    - 8989:8989 # sonarr
    - 7878:7878 # radarr
    - 9696:9696 # prowlarr
    - 8787:8787 # readarr
    - 8191:8191 # flaresolverr
    - 6789:6789 # nzbget
    - 80:80 # traefik
    - 8080:8080 # traefik dashboard
    - 8120:8118 # privoxy
    - 6800:6800 # aria
    - 6888:6888 # aria rpc
    - 6888:6888/udp
    - 6880:6880 # aria-web
    - 8265:8265 # tdarr webUI port
    - 8266:8266 # tdarr server port
    - 8096:8096 # jellyfin webgui
    - 8920:8920 # jellyfin optional
    - 7359:7359/udp # jellyfin optional
    - 1900:1900/udp # jellyfin optional
    - 61208:61208 # glances
    - 9712:80 # muximux
    - 53:53 # local dns server for *.docker

After **docker-compose up** or portainer stack start you should set you desktops **dns server to 127.0.0.1:53** this will enable you to open http://muxi.docker:9712 all other container interfaces should be visible here. if not all containers should be accesible with their **containername.docker** as long as your host dns is set to localhost.

there are 3 default vpn sessions, one for torrents one for usenet and one for web downloads via aria2. you can add **up to 5 concurrent sessions with one nordvpn account**.

for debugging purposes i included netshoot in the stack, a little vm to attach to different vpns or for filemanagement and cifs rights testing.

with glances you get a quick overview about your server and running containers.
should be **23** without portainer. **#alot**

##**REMINDER:** 

this is only the stack, internal configuration of any of the containers is not automated (yet), and has to be done by hand with the specific container ips in mind.
The whole purpose of this Project is to write a application that handels configuration of all containers in synergy.
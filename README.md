### Delete all (running/non-running) containers that match image name
```bash
docker rm -f $(docker ps -a | grep rabbitmq | awk '{print $1}')
```

### Delete all (running/non-running) containers
```bash
docker rm -f $(docker ps -aq')
```

### Delete all images
```bash
docker rmi -f $(docker images -aq)
```

### Docker Containers /etc/resolve.conf have a Google DNS Nameserver
https://docs.docker.com/engine/userguide/networking/default_network/configure-dns/

> Regarding DNS settings, in the absence of the --dns=IP_ADDRESS..., --dns-search=DOMAIN..., or --dns-opt=OPTION... options, Docker makes each container’s /etc/resolv.conf look like the /etc/resolv.conf of the host machine (where the docker daemon runs). When creating the container’s /etc/resolv.conf, the daemon filters out all localhost IP address nameserver entries from the host’s original file.

> Filtering is necessary because all localhost addresses on the host are unreachable from the container’s network. After this filtering, if there are no more nameserver entries left in the container’s /etc/resolv.conf file, the daemon adds public Google DNS nameservers (8.8.8.8 and 8.8.4.4) to the container’s DNS configuration. If IPv6 is enabled on the daemon, the public IPv6 Google DNS nameservers will also be added (2001:4860:4860::8888 and 2001:4860:4860::8844).

Docker by default will make the container's `/etc/resolv.conf` look like that of the host in the case DNS option is not passed. On my machine, my host's `/etc/resolv.conf` has `127.0.0.1`. Docker is smart enough to know that localhost in the container isn't localhost on the host, so it replaces it with the Google DNS ip addresses.

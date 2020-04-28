# Deb mirror

Setup local docker-based debian mirror.

## Commands

Build with docker:

    $ docker build -t aptmirror:latest .

Modify mirror.list to add repos.
Run this command to fetch files from apt, replace local file path with yours:
    
    $ docker run -v /volume1/common/apt-mirror-files/:/mnt/mirror/debian aptmirror:latest (Synology NAS)
    $ docker run -v /data/aptmirror-files/:/mnt/mirror/debian aptmirror:latest (Local Laptop)

Sync files with remote docker site (e.g. Synology NAS) if needed:
    $ rsync aptmirror-files/ admin@192.168.1.254:/volume1/common/ubuntu-apt-get-repo/apt-mirror-files/ -av -P

Now serve the files with your webserver of choice:
    
    $ docker run -p 8080:80 -v /volume1/common/apt-mirror-files/:/usr/share/nginx/html:ro -d nginx:alpine (Synology NAS)
    $ docker run -p 8080:80 -v /data/aptmirror-files/:/usr/share/nginx/html:ro -d nginx:alpine (Local Laptop)
    
## Edit Client to Use Mirror
Backup /etc/apt/sources.list
Modify /etc/apt/sources.list to local ip address where mirror is hosted
deb [arch=amd64] http://localhost/mirror/archive.ubuntu.com/ubuntu bionic universe
sudo apt-get update --allow-insecure-repositories

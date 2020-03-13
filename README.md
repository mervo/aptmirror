# Deb mirror

Setup local docker-based debian mirror.

## Commands

Build with docker:

    $ docker build -t aptmirror:latest .

Run this command to fetch files from apt, replace local file path with yours:
    
    $ docker run -v /volume1/common/apt-mirror-files/:/mnt/mirror/debian aptmirror:latest

Sync files with remote docker site if needed:
    $ rsync apt-mirror-files/ admin@192.168.1.254:/volume1/common/ubuntu-apt-get-repo/apt-mirror-files/ -av -P

Now serve the files with your webserver of choice:
    
    $ docker run -p 8080:80 -v /volume1/common/apt-mirror-files/:/usr/share/nginx/html:ro -d nginx:alpine
    
## Edit Client to Use Mirror
Backup /etc/apt/sources.list
Modify /etc/apt/sources.list to local ip address where mirror is hosted
deb [arch=amd64] http://localhost/mirror/archive.ubuntu.com/ubuntu bionic universe
sudo apt-get update --allow-insecure-repositories

# Deb mirror

Setup local docker-based debian mirror.

## Commands

Build with docker:

    $ docker build -t aptmirror:latest .


Run this command to fetch files from apt, replace local file path with yours:
    
    $ docker run -v /data/apt-mirror-files/:/mnt/mirror/debian aptmirror:latest

Now serve the files with your webserver of choice:
    
    $ docker run -p 80:80 -v /data/apt-mirror-files/:/usr/share/nginx/html:ro -d nginx:alpine
    
## Edit Client to Use Mirror
Backup /etc/apt/sources.list
Modify /etc/apt/sources.list to local ip address where mirror is hosted
deb http://localhost/archive.ubuntu.com/ubuntu bionic universe
sudo apt-get update --allow-insecure-repositories

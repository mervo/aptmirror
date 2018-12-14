# Deb mirror

Setup a simple docker-based (probably very unsecure) debian mirror for a local 
install fest.

Based on: https://medium.com/@moep_moep/linux-repository-mirror-with-docker-234c9a24e71e


## Commands

Build with docker:

    $ docker build -t aptmirror:latest .


Run it:
    
    docker run -v /path-to-local-files/:/mnt/mirror/debian aptmirror:latest
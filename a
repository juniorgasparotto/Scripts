#!/bin/bash
echo "start"

sudo apt update;
sudo apt install git;

sudo su - \
cat << EOF > /etc/docker/daemon.json
{
    "insecure-registries" : [ "172.30.0.0/16" ]
}
EOF
echo "1";
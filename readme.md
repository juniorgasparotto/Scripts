# Scripts

This repository is personal and aims to:

1) Help with my work with various scripts.
2) Helping others who have the same problems.

Feel free to contribute.

## Install OpenShift (Ubuntu 18.04.3 LTS)

1. Download Ubuntu Server ISO

http://releases.ubuntu.com/18.04.3/ubuntu-18.04.3-live-server-amd64.iso?_ga=2.167122174.1936246034.1573526752-2128499039.1567124980

2. Install Virtual Box or other 

3. Install Ubuntu Server

4. Execute this command (copy all and paste in console)

```
sudo apt update;
sudo apt install git;
git clone https://github.com/juniorgasparotto/Scripts.git;
sudo chmod +sx ./Scripts/openshift/install-openshift;
./Scripts/openshift/install-openshift;
```

5. Open in browser

https://192.168.0.113:8443

6. When restart PC

```
sudo oc cluster up --routing-suffix=192.168.0.113 --public-hostname=192.168.0.113;
sudo oc cluster up --routing-suffix=192.168.0.100 --public-hostname=192.168.0.100;
sudo oc cluster up --routing-suffix=192.168.0.21 --public-hostname=192.168.0.21 --host-data-dir="/mnt/files/data" --host-config-dir="/mnt/files/conf";

```

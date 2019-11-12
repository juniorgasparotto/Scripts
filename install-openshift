### Install Docker (https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository) OU https://get.docker.com/

sudo apt-get update
sudo apt-get install apt-transport-https;
sudo apt-get install ca-certificates;
sudo apt-get install curl;
sudo apt-get install gnupg-agent;
sudo apt-get install software-properties-common;
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88 
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo usermod -aG docker $USER

### Instal OpenShift (https://medium.com/@maheshacharya_44641/install-openshift-origin-on-ubuntu-18-04-7b98773c2ee6)

wget https://github.com/openshift/origin/releases/download/v3.9.0/openshift-origin-client-tools-v3.9.0-191fece-linux-64bit.tar.gz 
tar -zvxf openshift-origin-client-tools-v3.9.0-191fece-linux-64bit.tar.gz
cd openshift-origin-client-tools-v3.9.0-191fece-linux-64bit
sudo cp oc /usr/local/bin/
sudo su - \
cat << EOF > /etc/docker/daemon.json
{
    "insecure-registries" : [ "172.30.0.0/16" ]
}
EOF
service docker restart;
oc cluster up --routing-suffix=192.168.0.113 --public-hostname=192.168.0.113
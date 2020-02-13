# https://strimzi.io/quickstarts/okd/

#  Preparação

Busque pelo namespace "myproject" em todos os arquivos desta pasta e troque pelo nome do projeto no qual deseja instalar o kafka single.

find: myproject
replace: project-kafka

# Logar como admin

sudo su
oc login -u system:admin

oc new-project project-kafka
oc apply -f strimzi-cluster-operator-0.16.2.yaml -n project-kafka
oc apply -f kafka-persistent-single.yaml -n project-kafka

# Testando

oc wait kafka/my-cluster --for=condition=Ready --timeout=300s -n project-kafka
oc -n project-kafka run kafka-producer -ti --image=strimzi/kafka:0.16.2-kafka-2.4.0 --rm=true --restart=Never -- bin/kafka-console-producer.sh --broker-list my-cluster-kafka-bootstrap:9092 --topic my-topic
oc -n project-kafka run kafka-consumer -ti --image=strimzi/kafka:0.16.2-kafka-2.4.0 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning


# Acessar o Kafka de fora do servidor 

oc expose service my-cluster-zookeeper-client
my-cluster-zookeeper-client-myproject.192.168.0.10.nip.io

oc patch svc my-cluster-kafka-bootstrap -p '{"spec":{"externalIPs":["192.168.0.10"]}}'
oc patch svc my-cluster-zookeeper-client -p '{"spec":{"externalIPs":["192.168.0.10"]}}'

* Desativar o selinux: `/etc/sysconfig/selinux`

```
SELINUX=disabled
SELINUXTYPE=targeted
```

* Adiciona a porta do zookeper para ser acessada de fora do servidor

```
iptables -A INPUT -m state --state NEW -p tcp --dport 2181 -j ACCEPT
iptables -F
```

vim /etc/origin/master/master-config.yaml


oc expose service my-cluster-kafka-bootstrap
oc expose service my-cluster-zookeeper-client
oc get pods
oc port-forward my-cluster-kafka-0 2181:2181
oc port-forward my-cluster-zookeeper-0 9091:9091
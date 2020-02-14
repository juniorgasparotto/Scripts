
# Links importantes

* https://strimzi.io/quickstarts/okd/
* https://strimzi.io/docs/latest/full.html
* https://strimzi.io/2019/04/30/accessing-kafka-part-3.html
* https://github.com/strimzi/strimzi-kafka-operator/issues/128

# Preparação

Busque pelo namespace "myproject" em todos os arquivos desta pasta e troque pelo nome do projeto no qual deseja instalar o kafka single.

find: myproject
replace: project-kafka

# Instalação

```
sudo su
oc login -u system:admin

oc new-project project-kafka

oc create -f persistentvolume.kafka.yaml
oc apply -f strimzi-cluster-operator-0.16.2.yaml -n project-kafka
oc apply -f kafka-persistent-single.yaml -n project-kafka
```

# Testando

```
oc wait kafka/my-cluster --for=condition=Ready --timeout=300s -n project-kafka
```

```
oc -n project-kafka run kafka-producer -ti --image=strimzi/kafka:0.16.2-kafka-2.4.0 --rm=true --restart=Never -- bin/kafka-console-producer.sh --broker-list my-cluster-kafka-bootstrap:9092 --topic teste
```

```
oc -n project-kafka run kafka-consumer -ti --image=strimzi/kafka:0.16.2-kafka-2.4.0 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic teste --from-beginning
```

# Acessar o Kafka de fora do servidor

Libera o acesso externo via rotas (adiciona o listeners do tipo external igual a route)

* https://strimzi.io/2019/04/30/accessing-kafka-part-3.html

```
oc edit kafka my-cluster
```

1. Altere o conteudo do arquivo para adicionar o `listener -> external = route`
2. Mantenha o `listeners -> plain={}`, sem isso a chamada interna dentro do cluster via service para de funcionar

```yaml
spec:
  entityOperator:
    topicOperator: {}
    userOperator: {}
  kafka:
    config:
...
    listeners:
      external:
        type: route
      plain: {}
    replicas: 1
...
```

3. Obtenha o certificado para usar nos clientes

```
oc extract secret/my-cluster-cluster-ca-cert --keys=ca.crt --to=- > ca.crt
```


```
echo '{"kind": "ServiceAccount", "apiVersion": "v1", "metadata": {"name": "amq-service-account"}}' | oc create -f -
```

```
oc policy add-role-to-user view system:serviceaccount:hydro:amq-service-account
```

```
oc replace --force  -f amq-broker-7-image-streams.yaml
```

```
oc replace --force  -f amq-broker-78-persistence.yaml
```


```
oc new-app --template=amq-broker-78-persistence \
   -p AMQ_PROTOCOL=openwire,amqp,stomp,mqtt,hornetq \
   -p AMQ_QUEUES=demoQueue \
   -p AMQ_ADDRESSES=demoTopic \
   -p AMQ_USER=amq-demo-user \
   -p AMQ_PASSWORD=password \
   -p VOLUME_CAPACITY=1Gi
```
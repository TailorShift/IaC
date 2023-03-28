```

oc project atos-development

cat << EOF | oc apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: ubi9-tools
spec:
  terminationGracePeriodSeconds: 3
  containers:
    - name: ubi
      image: image-registry.openshift-image-registry.svc:5000/atos-development/ubi9-tools
      command:
        - bash
        - '-c'
        - |
          while true ; do sleep 2; done
EOF


oc delete pod ubi9-tools

oc exec ubi9-tools -i -t -- bash

alias ll='ls -al'

kafka-topics.sh --bootstrap-server=kafka-datacenter-kafka-bootstrap.atos-development.svc.cluster.local:9092 --list
kafka-topics.sh --bootstrap-server=kafka-datacenter-kafka-bootstrap.atos-development.svc.cluster.local:9092 --delete --topic '*.heartbeats'


KOPTS=--bootstrap-server=kafka-datacenter-kafka-bootstrap.atos-development.svc.cluster.local:9092
KOPTS=--bootstrap-server=kafka-backoffice-kafka-bootstrap.atos-shop-back-office.svc.cluster.local:9092

kafka-topics.sh $KOPTS --delete 
kafka-topics.sh $KOPTS --list |sort

kafka-topics.sh $KOPTS --delete --topic 'testtopic'
kafka-topics.sh $KOPTS --delete --topic 'mirrormaker2.*'
kafka-topics.sh $KOPTS --delete --topic 'mm2.*'
kafka-topics.sh $KOPTS --delete --topic '.*heartbeats'
kafka-topics.sh $KOPTS --delete --topic 'kafka-backoffice\..*'
kafka-topics.sh $KOPTS --delete --topic 'kafka-datacenter\..*'




```
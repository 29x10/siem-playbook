# SIEM Playbook Project

## Prerequisite

* python3.8 or newer
* pip3 installed
* pdm installed

## How to start

### Install pdm

```
python3 -m pip install pdm --user
```

### Install dependency

```
python -m pdm install
```

### Install collections


#### Install required collections

```
python3 -m pdm run ansible-galaxy collection install ansible.posix
python3 -m pdm run ansible-galaxy collection install community.general
python3 -m pdm run ansible-galaxy collection install community.crypto
```

you need to run beblow command everytime you update your local collection

```
python3 -m pdm run ansible-galaxy collection install $PWD/siem/ --force
```

### Run playbook


```
python3 -m pdm run ansible-playbook -i inventory/test/hosts playbooks/splunk.yml --tags "install"
```


### Verify Zookeeper

```
export CLIENT_JVMFLAGS="
-Dzookeeper.clientCnxnSocket=org.apache.zookeeper.ClientCnxnSocketNetty 
-Dzookeeper.client.secure=true 
-Dzookeeper.ssl.keyStore.location=~/workspace/cod/zookeeper/3.6.3/security/keystore.pem 
-Dzookeeper.ssl.keyStore.password=password 
-Dzookeeper.ssl.trustStore.location=~/workspace/cod/zookeeper/3.6.3/security/truststore.pem"

bin/zkCli.sh -server $HOSTNAME:2181
```

then check zk logs
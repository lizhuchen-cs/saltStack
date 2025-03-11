# Salt architecture

salt master
salt minions
formulas
grains
execution
pillar

### additional salt components:
top file
runners
returners
reactor
salt cloud
salt ssh

![Alt text](./images/salt%20architecture.PNG "Title")

## installation:
```
# install salt master
sudo apt install salt-master
sudo service salt-master status

# install salt minion
sudo apt install salt-minion
sudo service salt-minion status

```

configuration:
```
# edit minion configuration file
cd /etc/salt
sudo vim minion
master: master-ip(ip-127-0-0-1)

sudo service salt-minion restart
sudo service salt-minion status
```
### Agentless
check the salt minion registered to master:

```
sudo salt "*" test.ping
```

prerequisit:
```
sudo apt install python
# install pip
sudo curl 
sudo python get-pip.py
# install salt ssh
sudo pip install salt-ssh
cd /etc/salt && ls
sudo vim roaster
```
put below in roaster file
```
ID:
    host: 127.0.0.1
    # username of the host
    user: ubuntu
```
check if the agentless is working
```
salt-ssh -i "*" test.ping
```

### Grains

```
sudo salt "*" test.ping
# list all the grain information available in system
sudo salt "*" grains.ls
# get grains items details
sudo salt "*" grains.items
# ping all machines with ubuntu
sudo salt -G "os:ubuntu" test.ping

# minions cpu cores with cpuarch:x86_64 as the filter
sudo salt -G "cpuarch:x86_64" grains.item num_cpus
```

### SaltUtil
used to manage the state of minions

functions:
    running
    find_job: return specific data of job
    signal_job
    term_job
    kill_job

 Runner:
    functions:
        active
        lookup_jid
        list_jobs

### Salt components:
Salt master
    publisher
    eventpublisher
    mworker
Salt minion
    single process
    connects to master on tcp 4505 and 4506

runner, returner, reactor connect to eventbus, salt cloud

salt topology:
    Servers
    Pub/Sub
    Return

### salt runner

```
cd /etc/salt
sudo vim master
runner_dirs: [/home/ubuntu/runners]

sudo service salt-master restart

mkdir /home/ubuntu/runners
sudo vim test.py

```
test.py
```
import salt.client

def foo(outputter=None, display_prohress=False)
    print('hello salt')
    return 'working'
```
run the runner:

```
sudo salt-run test.foo

```

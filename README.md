Prerequisite
=====

You must be a root. To login as root, use command "sudo -i".


Build Docker Image
=====
#### 1. Build JBoss node docker image
```
$ cd jboss

$ sh -x build.sh
```

#### 2. Build collector docker image
```
$ cd ../collector

$ sh -x build.sh
```

#### 3. Build PostgreSQL docker image
```
$ cd ../postgresql

$ sh -x build.sh
```

Run Docker Container
=====
#### 1. Run Collector container
```
$ docker run -d -P --name=<Name of container> collector
```

#### 2. Run JBoss node container
```
$ docker run -d -P --name=<Name of container> jboss
```

#### 3. Run PostgreSQL container
```
$ docker run -d -P --name=<Name of container> postgresql
```

Connect to container
=====

#### 1. Check running docker container's ssh port
```
$ docker ps
```

#### 2. Connect to container via ssh. root's password is "password"
```
$ ssh localhost -p xxxxx
```

Modify collector server ip
=====

#### 1. Connect to JBoss node container
```
$ ssh localhost -p xxxxx
```

#### 2. Modify td-agent.conf
Modify ip address at line 20.

ex) host 172.17.0.32
```
$ vi /etc/td-agent/td-agent.conf
```

#### 3. Restart td-agent
```
$ /etc/init.d/td-agent restart
```

Put log and check
=====

#### 1. Put sample data to dump.log at "JBoss Container"
```
$ echo 'T001,select' >>  /var/log/td-agent/dump.log
```

#### 2. Check metering log at "Collector Container"
```
$ tail -f /var/log/td-agent/metering.<YYYYMMDD>.log
```

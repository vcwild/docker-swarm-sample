
## Backup Docker Swarm

Using Docker Machine & Docker Swarm

```{sh}
docker-machine ssh [docker machine]
```

While in the Docker Swarm manager node:

- Change to super user

```{sh}
sudo su
```

- Copy the following folder and save it as backup

```{sh}
cp -r /var/lib/docker/swarm backup
```

## Restore Docker Swarm

While in the Docker Swarm manager node

- Copy the backup folder to Docker Swarm

```{sh}
cp -r backup/* /var/lib/docker/swarm 
```

- Restart the cluster

```{sh}
docker swarm init --force-new-cluster --advertise-addr [ip address]
```

## How to format Docker Node output 

- For Host and Manager status

```{sh}
docker node ls --format "HOST: {{.Hostname}} MAN: {{.ManagerStatus}}"
```
## Create service 

```{sh}
docker service create --name [service-name] --replicas [n-replicas] -p [bind-address]:[container-address] [image]
```

### Global mode

- Global mode will replicate the service in all nodes

```{sh}
docker service create --name [service-name] -p [bind-address]:[container-address] --mode global [image]
```


## How to stop all Docker services

While in a Docker Swarm manager node

```{sh}
docker service rm $(docker service ls -q)
```

## How to avoid service attribution to a node

```{sh}
docker node update --availability drain [hostname]
```

## How to list all services being executed

```{sh}
docker service ps $(docker service ls -q)
```

## How to add service role constraints

Service can only be executed in worker nodes

```{sh}
docker service update --constraint-add node.role==worker [service-id]
```

Service can only be executed in the following node id

```{sh}
docker service update --constraint-add node.id==[node-id] [service-id]
```

Service can only be executed in the following host
```{sh}
docker service update --constraint-add node.hostname==[host-name] [service-id]
```

## How to remove service role constraints


```{sh}
docker service update --constraint-rm node.id==[node-id] [service-id]

docker service update --constraint-rm node.hostname==[host-name] [service-id]
```

## Create service replicas

- Using service update

```{sh}
docker service update --replicas [n-replicas] [service-id]
```
- ALT: Using service scale

```{sh}
docker service scale [service-id]=[n-replicas]
```

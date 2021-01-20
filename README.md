
## Backup Docker Swarm

### Using Docker Machine & Docker Swarm

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

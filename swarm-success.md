### Create docker-machine remote connection
```
docker-machine create --driver generic \
--generic-ip-address=${nodes.cp.master.intIP} \
--generic-ssh-key ~/.ssh/id_rsa \
--engine-storage-driver overlay ${env.envName}
```

### Connect to the environment
```
eval $(docker-machine env ${env.envName})
```

### Add a Manager node to the cluster
```
docker swarm join --token \
${globals.manager_token} \
${nodes.cp.master.intIP}:2377
```

### Add a Worker node to the cluster
```
docker swarm join --token \
${globals.worker_token} \
${nodes.cp.master.intIP}:2377
```

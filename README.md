# Minio with Docker

Minio is an open source object storage server with Amazon S3 compatible API. 
Build cloud-native applications portable across all major public and private clouds.

# Run Standalone Minio on Docker

```bash
docker run -p 9000:9000 --name minio1 \
  -e "MINIO_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE" \
  -e "MINIO_SECRET_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" \
  -v /mnt/data:/data \
  -v /mnt/config:/root/.minio \
  minio/minio server /data
```

- Create your own ACCESS_KEY and SECRET_KEY

#  Run Distributed Minio on Docker Compose

## Prerequisites

- [Install Docker Compose](https://docs.docker.com/compose/install/)
- [Get Overview of Docker Compose](https://docs.docker.com/compose/overview/)

## Run with docker-compose

```bash
docker-compose up -d
```

Each instance is now accessible on the host at ports 9001 through 9004, proceed to access the Web browser at <http://127.0.0.1:9001/>


# Deploy Minio on Docker Swarm

## Prerequisites

- [Install Docker Compose](https://docs.docker.com/compose/install/)
- [Get Overview of Swarm mode key concepts](https://docs.docker.com/engine/swarm/key-concepts/)
- Read Through [Getting started with swarm mode](https://docs.docker.com/engine/swarm/swarm-tutorial/)

##  Create a Swarm Cluster

- Go through the swarm cluster creation [Create a swarm](https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/).


## Create Docker secrets for Minio or remove the secret in .yml file and set th environment 

```bash
echo "AKIAIOSFODNN7EXAMPLE" | docker secret create access_key -
echo "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" | docker secret create secret_key -
```

## run

```bash
docker stack deploy --compose-file=minio-stack.yaml minio
```

OR

```bash
docker stack deploy -c minio-stack.yaml minio
```

## check the status of the stack

#### list stack

```bash
docker stack ls
```

#### list services

```bash
docker service ls
```

#### check logs of the service

```bash
docker service logs <Service_ID>
```

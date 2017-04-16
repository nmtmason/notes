# Docker

## Installation

For Ubuntu, [follow the instructions](https://docs.docker.com/engine/installation/linux/ubuntu/) to install Docker.

```
curl -sS https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
sudo apt-get update
sudo apt-get install docker-ce
```

## PostgreSQL

Use the [official docker postgres image](https://hub.docker.com/_/postgres/) to start a PostgreSQL instance using docker.

```
sudo docker run --name container-name -e POSTGRES_PASSWORD=password -d postgres -p 5432:5432
```

Connect to a `psql` session.

```
sudo docker run -it --rm --link container-name:postgres postgres psql -h postgres -U postgres
```

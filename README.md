# Containerization of Java app using Docker

- Create a deployment instance in AWS using Ubuntu 24.04. 
- Name it as `deploy`
- use `t2.medium` for better performance.
- SSH to `deploy` instance
``` 
ssh -i xxx.pem ubuntu@<ip address>
```
- Install Docker
- https://docs.docker.com/engine/install/ubuntu/
- Set up Docker's `apt` repository

```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl -y
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

- Install the Docker packages.

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

- Manage Docker as a non-root user

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

- Relogin console to update groups in list

```bash
groups
```

- Verify that the Docker Engine installation is successful by running the `hello-world` image.

```bash
docker run hello-world
```

- Reset docker

```bash
docker system prune -a
```

- Create containerize-java-docker repository from GitHub
- Git clone repo

```bash
cd
mkdir -p git
cd git
git clone https://github.com/ahmdnzm/containerize-java-docker.git
cd containerize-java-docker
git branch -a
```

- Change to `containers` branch

```bash
git checkout containers
```
### Review Dockerfile

- Review App Dockerfile in `Docker-files > app` directory
- Review DB Dockerfile in `Docker-files > db` directory
- Review Web Dockerfile in `Docker-files > web` directory

- Review Docker compose file `docker-compose.yml`


- Run `docker compose build` to build the images

```bash
docker compose build
```

- Bring up the docker compose

```bash
docker compose up -d
```
- login to the website using public IP

### Troubleshooting

- Check db container
```bash
docker exec -it <db container id> /bin/bash
```
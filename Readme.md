# Manifest for deploying Nexus Package Registry

## Getting started
Requirements:
- docker 

1. Create your certs in ./nginx/certs. Finally you must have registry.crt, registry.csr and registry.key in there
2. Run `docker compsoe up -d` 
3. Head to http://[your-server-address]. You must be able to see the landing page of Nexus 
4. After the container were created, get admin password with `docker exec -it nexus cat /nexus-data/admin.password`
5. Log into the dashboard, then from Settings (on the sidebar) create your repos, roles and users.
6. To make authentication methods available you must head to `Settings -> Security -> Realms`

### NOTE:
When working with docker volumes on the same directory make sure the UID inside the container has the permissions to write on the host's volume 
```sh
sudo chown -R 200:200 ./nexus-data
```

## Set up local Docker registry
1. Head to docker(hosted) page to create the repo
2. On the `Connector` section add your http and/or https ports (you have to update `docker-compose.yml.services.registry.ports` to make this work 
3. Head to settings -> Security-> Realms and add `Docker Bearer Token Realm`
4. Click save
### How to push and pull
If you do not use HTTPS add this to your /etc/docker/daemon.json:
```json
{
...
"insecure-registries" : ["<nexus-server-address>:<your-repo-connector-port"]
...
}
```
Then run
```
sudo systemctl daemon-reload && sudo systemctl restart docker
```
Tag your image like 
```
docker tag busybox:latest 172.16.110.116:5000/repository/my-docker-repo/test:latest
```
Then login:
```
docker login 172.16.110.116:5000 -u <username>
```
Then you can push the image there.

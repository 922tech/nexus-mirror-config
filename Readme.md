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
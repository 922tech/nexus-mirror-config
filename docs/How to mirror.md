## Mirroring APT Registry
### Server side:
Create a proxy repository.
Options:
- _Location of the remote repository being proxied_: http://deb.debian.org/debian

- Make sure the artifacts are **cached** by checking option: _Cache responses for content not present in the proxied repository_
- _How long (in minutes) to cache **artifacts** before rechecking the remote repository. Release repositories should use -1.*_ ----> (-1 means forverer)
- _How long (in minutes) to cache **metadata** before rechecking the remote repository._
* **NOTE**: Make sure life of metadata is longer than artifacts' life

### Client Side: 
```
sudo nano /etc/apt/auth.conf.d/registry.conf
sudo chmod 600 /etc/apt/auth.conf.d/registry.conf
```
Put inside the file(username=admin, password=1qaz!QAZ):
```
machine http://registry.dshasin.net
login admin 
password 1qaz!QAZ
```
If the repo uses HTTPS with a valid CA you can write `machine http://registry.dshasin.net`. 

You can either put the CA in the trusted CAs of your client machine

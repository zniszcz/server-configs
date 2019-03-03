# DevOps - Server utils

## Prerequirements

### DNS configuration

I assume you have digital ocean server and domain bough on ovh.

#### 1. Setup NS servers
On ovh panel go to `Web -> Domains -> your-domain.com -> DNS Servers`. Add three records:
```
ns1.digitalocean.com
ns2.digitalocean.com
ns3.digitalocean.com
```

Yes. Without IP adresses.

#### 2. Setup domain on DO
Go to DigitalOcean panel, then `Networking`. Add domain and choose droplet from list.

#### 3. Setup DNS on DO
Add aggregated record. Hostname: `@` and will redirect to your droplet.

#### 4. Make sure you can handle subdomains.
Add another aggregated record. Hostname `*` and will redirect also to your droplet.

#### 5. Wait
It could took a while to refresh propagate DNS servers update.

### Droplet configuration

I assume you have [docker](https://www.docker.com/) and [nginx](https://www.nginx.com/) installed. And also you have working on ubuntu (when I'm writing this doc I'm using ubuntu 18.04).

Following soft need a few more packages to run:

* `curl`
* `openssl` (managing htpasswd's)
* `apache2-utils` (also managing htpasswd's)
* `apt-transport-https`
* `ca-certificates`
* `software-properties-common`

### Trusted links

* [Installing docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)
* [Installing nginx](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)
* [Simple authentication on nginx servers](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-nginx-on-ubuntu-14-04)
* [Setup Let's encrypt](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)

## Installation
Execute following files __**from this directory**__.

### 1. Binding `sites-available`
Remove `/etc/nginx/sites-available` and link this one from repository.

```
sudo rm -r /etc/nginx/sites-available
sudo ln -s "$(pwd)/sites-available" /etc/nginx/sites-available
```

### 2. Add symlinks to `int` and `test` stages
Links stages configs to stages directory main files.
```
ln -s "$(pwd)/int/nginx.config" "$(pwd)/sites-available/int"
ln -s "$(pwd)/test/nginx.config" "$(pwd)/sites-available/test"
```

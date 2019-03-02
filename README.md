# DevOps - Server utils

## Prerequirements
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

## Installation

### Add symlinks to `int` and `test` stages
Execute following files **from this directory**.
```
ln -s "$(pwd)/int/nginx.config" "$(pwd)/sites-available/int"
ln -s "$(pwd)/test/nginx.config" "$(pwd)/sites-available/test"
```

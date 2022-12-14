# Adding ldap auth module to nginx official image
This is the Git repo which fork from [official nginx](https://registry.hub.docker.com/_/nginx/) and add ldap auth module [nginx-auth-ldap](https://github.com/kvspb/nginx-auth-ldap).

## Build

```
$ cd modules
$ docker build --build-arg ENABLED_MODULES="auth_ldap" -t my-nginx-with-ldap-auth .
```
This command will attempt to build an image called `my-nginx-with-ldap-auth` based on
official nginx docker hub image with [nginx-auth-ldap](https://github.com/kvspb/nginx-auth-ldap) module.
By default, a Debian-based image will be used.  If you wish to use Alpine
instead, add `-f Dockerfile.alpine` to the command line(and replace libldap-dev with openldap-dev in file modules/auth_ldap/build-deps).

## Usage

Load ngx_http_auth_ldap_module.so in file nginx.conf.

```
user  nginx;
worker_processes  auto;

load_module "/usr/lib/nginx/modules/ngx_http_auth_ldap_module.so";

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;

events {
    worker_connections  1024;
}

```

and follow the README of [nginx-auth-ldap](https://github.com/kvspb/nginx-auth-ldap).

Good luck.

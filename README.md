# Craft 3 Docker Boilerplate

This is a Craft 3 boilerplate project environment with Docker.

## Features

- PHP 7.3
- NGINX 1.17 with caching configuration and security enhancement
- MariaDB 10.4
- Gulp

## To start

```
$ git clone https://github.com/antoniojhun/craftbox.git
$ cd craftbox
$ docker-compose up -d
```

[http://localhost/admin](http://localhost/admin)


In development, comment line 62 and uncomment line 64 of docker-compose.yml to activate, 
```
$ command: ["./node_modules/.bin/gulp", "watch"]
```

Gulp watch command will look up source files in /src/assets directory

If template files are cached in development mode, set /nginx/default.conf line 21 $no_cache value to 1
```
set $no_cache 1;
```



### Requirements
[Docker](https://www.docker.com)

### Default

Change default settings in docker-compose.yml to fit however you like

| Container Info     |                      |
| ------------------ | -------------------- |
| Docker Containers: | nginx, php, database, buildpackage |
| Site Port:         | 80                 |
| Database Port:     | 3306                 |

| Default DB settings when installing     |                    |
| ---------------------- | ------------------ |
| Server:                  | database      |
| Username:              | starter              |
| Password:              | secr3te!          |
| Database:      | projectA            |

### Inspiration

Hat tip to Chris Lee(https://github.com/chrisleekr), Matt Gray(https://github.com/mattgrayisok/), Andrew Welch(https://github.com/nystudio107/)

### To Do
- [ ] Update PHP to 7.4
- [ ] Update composer.json - Craft, PHP env
- [ ] Update Craft to 3.7
- [ ] Update compatible Craft Plugins for Craft 3.7
- [ ] Update Gulp
- [ ] Scope a project using Craft 4 with Vite :tada:

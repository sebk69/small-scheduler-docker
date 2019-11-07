# Small Scheduler Docker
#### A docker environment for [Small Scheduler](https://github.com/sebk69/small-scheduler)

## Install development version

#### Dependencies

On Ubuntu or Debian :
``` bash
$ sudo apt-get install git
```

See [docker install documentation](https://docs.docker.com/install/linux/docker-ce/ubuntu) to install docker

See [docker-compose documentation](https://docs.docker.com/compose/install) to install docker-compose

#### Clone this repo and build docker environement

``` bash
$ git clone --recurse-submodules git@github.com:sebk69/small-scheduler-docker.git
$ cd small-scheduler-docker/commands
$ ./install
```

Answer questions of the install script and build docker environment :
``` bash
$ ./rebuild-docker
```

Download symfony dependencies
``` bash
$ ./composer update
```

Create database
``` bash
$ ./console sebk:small-orm:layers-execute
```

Create first user
``` bash
$ ./console sebk:small-user:create-user [email] [nickname] [password]
$ ./console sebk:small-user:add-role [nickname] ROLE_ADMIN
```

#### Run scheduler
``` bash
$ ./schedule
```

#### Run webapp to configure your server

Finaly start development webapp
``` bash
$ ./npm install
$ ./ng serve --host 0.0.0.0
```

Go to http://localhost:4200 to login.

#### Install clients to consume tasks

See [sebk69/small-scheduler-client](https://github.com/sebk69/small-scheduler-client) to install client across your cloud servers and consume tasks.

## TODO : Install production environement documentation

## percona-xtrabackup Dockerfile


This repository contains **Dockerfile** of [percona-xtrabackup](https://www.percona.com/software/mysql-database/percona-xtrabackup) for [Docker](https://www.docker.com/)'s [automated build](https://registry.hub.docker.com/u/igortimoshenko/docker-percona-xtrabackup/) published to the public [Docker Hub Registry](https://registry.hub.docker.com/).


### Base Docker Image

* [igortimoshenko/docker-cron-job](https://hub.docker.com/igortimoshenko/docker-cron-job/)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Download [automated build](https://registry.hub.docker.com/u/igortimoshenko/docker-percona-xtrabackup/) from public [Docker Hub Registry](https://registry.hub.docker.com/): `docker pull igortimoshenko/docker-percona-xtrabackup`

   (alternatively, you can build an image from Dockerfile: `docker build -t="igortimoshenko/docker-percona-xtrabackup" github.com/igortimoshenko/docker-percona-xtrabackup`)


### Usage

Start container specifying the executable script for cron:

    docker run -d \
    -v `<script-dir>`/script.sh:/root/script.sh \
    -e CRON_JOB='* * * * * ~/script.sh >> /var/log/script.log 2>&1' \
    -e HOST="mysql" \
    -e PORT="3306" \
    -e USER="mysql" \
    -e PASS="mysql" \
    --link mysql:mysql \
    igortimoshenko/docker-percona-xtrabackup    

> Note that if you need environment variables within your cron script then
> include the following line `source /root/.env-vars` in your script

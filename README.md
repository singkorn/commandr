# tr_online-v2 for Docker

- [Requirements](#requirements)
- [Installation](#installation)
- [Commands](#commands)

## Requirements

- [Docker 17.06+](https://www.docker.com/community-edition)

## Installation

First, login to Docker registry, by running this command and enter your GitLab credential:

    docker login scm.trendvg3.com:4567

Clone tr_online-v2 from GitLab

    git clone git@scm.trendvg3.com:suntunz/tr_online-v2.git

Build docker:

    docker build -t "next1" .

Start docker, App will running on port 3000:

    docker run -it -p 3000:3000 "next1"

Start docker and set 4 instances of PM2 in cluster mode:

    docker run -it -p 3000:3000 -e INSTANCE=4 "next1"

Start docker, set 4 instances of PM2 in cluster mode and add host for connect:

    docker run -it -p 3000:3000 -e INSTANCE=4 --add-host connect.thairath.co.th:172.17.0.1 "next1"

## Commands

Start the docker in background:

    docker run -d "next1"

List containers:

    docker ps

Stop one or more running containers:

    docker stop [CONTAINER ID]

Start docker in interactive mode:

    docker run -it -p 3000:3000 "next1"

Start docker in interactive mode and get bash into container:

    docker run -it -p 3000:3000 "next1" bash

## Change logs

Click to read [changelogs](CHANGELOG.MD)

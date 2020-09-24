# Useful Commands

- [Git](#git)
- [Docker](#docker)
- [Sonarqube](#sonarqube)

# Git

List all branches with latest commit order by ascending:

    git for-each-ref --sort=-committerdate refs/heads/ --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(color:red)%(objectname:short)%(color:reset) - %(contents:subject) - %(authorname) (%(color:green)%(committerdate:relative)%(color:reset))'

List all branches and then fetch or pull:

    git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
    git fetch --all
    git pull --all

# Docker

## Run OWASP ZAP Full Scan on docker
docker run -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-stable zap-full-scan.py \
    -t https://www.thairath.dev/home -g gen.conf -r thairath_dev_testreport.html

## Delete docker images by grepping docker names
docker images -a | grep "<none>" | awk '{print $3}' | xargs docker rmi

## Force delete docker images by grepping CREATED
docker rmi --force \
    $(docker images --format '{{.Repository}}:{{.Tag}}:{{.CreatedSince}}' | grep ${IMAGE} | grep 'weeks ago\|months ago\|years ago' | cut -f 1-2 -d ':')

## Find ID of dependent image upon parent image
docker inspect --format='{{.Id}} {{.Parent}}' $(docker images --filter since=<imageId> -q)

# SonarQube

    docker run \
        --rm \
        -e SONAR_HOST_URL="http://${SONARQUBE_URL}" \
        -v "${YOUR_REPO}:/usr/src" \
        sonarsource/sonar-scanner-cli

    docker run \
        --rm \
        -e SONAR_HOST_URL="http://localhost:9000" \
        -v "/Users/user/Documents/workspace/tr-online:/usr/src" \
        sonarsource/sonar-scanner-cli

    URL: https://sonarqube.sngkrn.xyz/projects
    Token: tr-online-api-phalcon: aeb7a83b92853d532d19bbfac508461c641c3b78

    sonar-scanner \
    -Dsonar.projectKey=tr-online-api-phalcon \
    -Dsonar.sources=. \
    -Dsonar.host.url=https://sonarqube.sngkrn.xyz \
    -Dsonar.login=aeb7a83b92853d532d19bbfac508461c641c3b78 \
    -Dsonar.verbose=true

    sonar-scanner \
    -Dsonar.projectKey=tr-online-v2-nextjs \
    -Dsonar.sources=. \
    -Dsonar.host.url=https://sonarqube.sngkrn.xyz \
    -Dsonar.login=e0d7208b1834b940c3de06a340de30aec22ff6f1 \
    -Dsonar.verbose=true


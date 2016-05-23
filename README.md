# travix/gocd-server

[SonarQube](http://www.sonarqube.org/) code quality analysis

[![Stars](https://img.shields.io/docker/stars/travix/sonarqube.svg)](https://hub.docker.com/r/travix/sonarqube/)
[![Pulls](https://img.shields.io/docker/pulls/travix/sonarqube.svg)](https://hub.docker.com/r/travix/sonarqube/)
[![License](https://img.shields.io/github/license/Travix-International/docker-sonarqube.svg)](https://github.com/Travix-International/docker-sonarqube/blob/master/LICENSE)

# Usage

To run this docker container use the following command

```sh
docker run -d -p 9000:9000 travix/sonarqube:latest
```

# Environment variables

In order to configure the server with other than default settings you can pass in the following environment variables

| Name                    | Description                         | Default value                      |
| ----------------------- | ----------------------------------- | ---------------------------------- |
| SONARQUBE_JDBC_USERNAME | Username for accessing the database | sonar                              |
| SONARQUBE_JDBC_PASSWORD | Password for accessing the database | sonar                              |
| SONARQUBE_JDBC_URL      | The url to connect to the database  | jdbc:h2:tcp://localhost:9092/sonar |

Start the container by passing in environment variables in the following manner

```sh
docker run -d \
    -p 9000:9000 \
    -e "SONARQUBE_JDBC_USERNAME=sonar" \
    -e "SONARQUBE_JDBC_PASSWORD=sonar" \
    -e "SONARQUBE_JDBC_URL=jdbc:h2:tcp://localhost:9092/sonar" \
    travix/sonarqube:latest
```

# Mounting volumes

In order to keep important data persisted over a restart can mount the following directories

| Directory                 | Description                         | Importance                                                                        |
| ------------------------- | ----------------------------------- | --------------------------------------------------------------------------------- |
| /opt/sonarqube/extensions | Downloaded and installed extensions | Without saving this to a persistent disk the extensions are lost on every restart |

Start the container like this to mount the volume

```sh
docker run -d \
    -p 9000:9000 \
    -e "SONARQUBE_JDBC_USERNAME=sonar" \
    -e "SONARQUBE_JDBC_PASSWORD=sonar" \
    -e "SONARQUBE_JDBC_URL=jdbc:h2:tcp://localhost:9092/sonar" \
    -v /mnt/persistent-disk/sonarqube/extensions:/opt/sonarqube/extensions \
    travix/sonarqube:latest
```
# Spring PetClinic CI/CD Pipeline with GitHub Actions and Docker

## Project Overview

This project demonstrates a CI/CD workflow for the Spring PetClinic Java
application. GitHub Actions verifies the Maven project using Java 17,
builds a Docker image, and publishes the image to Docker Hub on pushes
to the `main` branch.

## Technology Stack

-   Java 17
-   Maven Wrapper
-   Spring Boot / Spring PetClinic
-   Docker and Docker Desktop
-   GitHub Actions
-   Docker Hub

## Repository and Image

-   **GitHub repository:**
    https://github.com/yash02604/CI-CD-Pipeline-with-GitHub-Actions-Docker
-   **Docker Hub image:**
    https://hub.docker.com/r/yash2608/spring-petclinic
-   **Image tag:** `yash2608/spring-petclinic:latest`

## CI/CD Workflow

1.  GitHub Actions checks out the repository.
2.  It configures Java 17 and Maven dependency caching.
3.  It runs `./mvnw -B verify`.
4.  It configures Docker Buildx.
5.  On a push to `main`, it logs in to Docker Hub using GitHub
    repository secrets.
6.  It builds the Docker image and pushes
    `yash2608/spring-petclinic:latest`.
7.  Pull requests run the verification and image build without
    publishing the image.

### Required GitHub Secrets

Configure these under **Settings → Secrets and variables → Actions**: -
`DOCKERHUB_USERNAME` --- Docker Hub username (`yash2608`) -
`DOCKERHUB_TOKEN` --- Docker Hub access token with repository read/write
permissions

Never put access tokens directly in the workflow file or commit them to
Git.

## Run the Published Image

Prerequisite: Docker Desktop is running.

``` powershell
docker pull yash2608/spring-petclinic:latest
docker run -d --name petclinic-test -p 8083:8080 yash2608/spring-petclinic:latest
```

Open http://localhost:8083 in a browser.

To view logs:

``` powershell
docker logs petclinic-test
```

To stop and remove the test container:

``` powershell
docker stop petclinic-test
docker rm petclinic-test
```

If the name or port is already in use, choose another container name or
unused host port.

## Evidence / Screenshots

Add your own screenshots to a `screenshots/` folder and update this
list: 1. `screenshots/github-actions-success.png` --- successful
**PetClinic CI/CD - Docker Hub** workflow run. 2.
`screenshots/docker-hub-latest.png` --- Docker Hub repository showing
the `latest` tag. 3. `screenshots/petclinic-localhost.png` --- PetClinic
application open at `http://localhost:8083`.

## Project Outcome

The application was built into a Docker image, published to Docker Hub,
and pulled and run locally from the published image. The GitHub Actions
workflow automates Maven verification and Docker image publishing.

## Scope and Limitations

This project demonstrates CI and container-image delivery. It does not,
by itself, demonstrate deployment to AWS, Kubernetes, or another
production hosting environment. The `latest` tag is used for the
published image; production workflows would typically also publish
immutable version tags.

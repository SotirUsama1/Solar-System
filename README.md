# Solar-System

## Sprint 5 - Task 1 - Containerize App & Push to Docker Hub via CI/CD

> <b>Task Description:</b> <br>
> Create a Dockerfile for the app, build and test locally, then set up a CI workflow (e.g., GitHub Actions) that builds the image on push to main, tags it, and pushes it to Docker Hub.

In this Task, I used a simple HTML+MongoDB+NodeJS project to display Solar System and it's planets, the repo link [`solar-system` by sidd-harth](https://github.com/sidd-harth/solar-system/tree/main).

---

### 1. Set Environment variables and secrets

This step for correct running. <br>
Setup the secrets and variables on github actions variables and secrets each according to its type in the following table with values stored in [`mongo.env`](./mongo.env) and [`dockerHub.env`](./dockerHub.env) ignored files from docker image and github repo but transfered off cloud for security

| name               | type     | value       |
|--------------------|----------|-------------|
| MONGO_USERNAME     | var      | superuser   |
| MONGO_PASSWORD     | secret   | *           |
| DOCKER_USERNAME    | secret   | *           |
| DOCKER_PATOKEN     | secret   | *           |

---

### 2. Run a docker container of this image

* login with docker credentials stored in [`dockerHub.env`](./dockerHub.env) file where the container is desired to run on using these commands
``` sh
docker login -u <DOCKER_USERNAME>
```
when you are prompted to enter password paste `DOCKER_PATOKEN`

* Run a new container of the solar-system nodejs app image
``` sh
docker run --env-file mongo.env \
-p 3000:3000 sotirusama/solar-system:latest
```
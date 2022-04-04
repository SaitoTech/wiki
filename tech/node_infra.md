---
title: Start a node
description: This page served for how to start nodes from Docker and it also includes some explanation for Dockerfile.
published: true
date: 2022-01-26T07:31:15.815Z
tags: 
editor: markdown
dateCreated: 2021-11-29T08:23:51.595Z
---

# Bare metal
- If you don't want to use Docker setup, basically just need to run the node via [README](https://github.com/SaitoTech/saito-rust#run-the-node) on our main Saito Rust repository.

# Docker / Docker Compose

## Introduction
Our local development environment and our production environment serve two very different purposes. Currently we used Docker & Docker Compose to serve for a test network on the Rust side with 2 or more peers connect & synchronize data. 

## Prerequisites
- [Docker](https://docs.docker.com/engine/install/) 
- [Docker Compose](https://docs.docker.com/compose/install/)

## Start nodes
- Try this to build our Docker image we attached a tag to it: 
```
# Build a docker image tagged as "saito-app" according to the recipe
# specified in `Dockerfile`
docker build --tag saito-app --file Dockerfile .
```
What does the `.` at the end of the command stand for?
`docker build` generates an image starting from a recipe (the [`Dockerfile`](https://github.com/SaitoTech/saito-rust/blob/main/Dockerfile)) and a build context. You can picture the Docker image you are building as its own fully isolated environment. 
The only point of contact between the image and your local machine are commands like `COPY` or `ADD`: the build context determines what files on your host machine are visible inside the Docker container to `COPY` and its friends.

- If you dont want to do this, just use docker-compose, it will build & start your nodes. Try this command from your favorite terminal:
```
CONF_FILE=config_file_path W_PWD=password_string docker-compose -f docker-compose.test.yml up -d --build
```
For now, we just support `docker-compose.test.yml` for network tests, therefore there are no `docker-compose.yml` to actually run nodes on PRODUCTION. That's why you need to add the parameter `-f` in command above.

What are `CONF_FILE` & `W_PWD`? If you look at the [`docker-compose.test.yml`](https://github.com/SaitoTech/saito-rust/blob/main/docker-compose.test.yml) file, you can easy-find these variables. 
- `CONF_FILE` is the peer configuration file - in this case it is `configuration/peers.yml`.
- `W_PWD` is the wallet password - in this case it is `asdf`.

Why i didnt put them directly into that `docker-compose` file? Because they're sensitive values and we want flexible to fill it by ourselves - via cli parameters and only we know it. Another reason, we can easy-configure via github ci vars once we need.

## Some docker utils commands
- check nodes up & running: `docker ps`
- view the saito nodes logs: 
```
docker logs saito_app        # view logs on node 1
docker logs saito_app_node1  # view logs on node 2
...
```
- Stop your nodes: `docker stop saito_app saito_app_node1`

## Next step: could be an Ansible setup for this - I made [this repo](https://github.com/SaitoTech/saito-rust-deployment) based on Richard's requirements, was set it up & running on my DO instance. So I can prove it work if anyone used it for deployment.
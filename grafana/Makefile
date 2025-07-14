# Makefile for Grafana Docker container

IMAGE_NAME=grafana-gbo
CONTAINER_NAME=grafana-gbo
PORT=3000

.PHONY: build up down logs

build:
	docker build -t $(IMAGE_NAME) .

up:
	docker run -d --name $(CONTAINER_NAME) -p $(PORT):3000 $(IMAGE_NAME)

down:
	docker stop $(CONTAINER_NAME) || true
	docker rm $(CONTAINER_NAME) || true

logs:
	docker logs -f $(CONTAINER_NAME) 
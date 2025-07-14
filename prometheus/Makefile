IMAGE_NAME=prometheus-gbo
CONTAINER_NAME=prometheus-gbo
PORT=9090

.PHONY: build up down restart logs clean

build:
	docker build -t $(IMAGE_NAME) .

down:
	docker stop $(CONTAINER_NAME) || true
	docker rm $(CONTAINER_NAME) || true

up:
	docker run -d --name $(CONTAINER_NAME) -p $(PORT):9090 $(IMAGE_NAME)

restart: down up

logs:
	docker logs -f $(CONTAINER_NAME)

clean:
	docker stop $(CONTAINER_NAME) || true
	docker rm $(CONTAINER_NAME) || true
	docker system prune -f
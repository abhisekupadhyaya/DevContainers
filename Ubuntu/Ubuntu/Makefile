.PHONY: build run clean

build:
	docker build -t ubuntu -f Dockerfile .

run: build
	docker run -d -p 8833:8833 --name ubuntu ubuntu

clean:
	docker stop ubuntu || true
	docker rm ubuntu || true
	docker rmi ubuntu || true 
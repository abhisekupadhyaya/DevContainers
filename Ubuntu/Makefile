.PHONY: build clean

build:
	cd Ubuntu && make build
	docker-compose up -d

clean:
	docker-compose down
	docker rmi ubuntu || true 
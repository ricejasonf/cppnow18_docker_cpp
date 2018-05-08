image_train:
	docker build --rm -t docker_train .
train:
	docker run --rm -v ${shell pwd}/target:/opt/target docker_train

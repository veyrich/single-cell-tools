IMAGE_NAME="base"
IMAGE_TAG="latest"

build:
	docker build -t $(IMAGE_NAME):$(IMAGE_TAG) .

build-nocache:
	docker build --no-cache -t $(IMAGE_NAME):$(IMAGE_TAG) .

run:
	docker run -it --rm $(IMAGE_NAME):$(IMAGE_TAG)

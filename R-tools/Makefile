#Base image plus Seurat / Dynamo

IMAGE_NAME="sctools"
IMAGE_TAG="latest"

build:
	docker build -t $(IMAGE_NAME):$(IMAGE_TAG) .

build-nocache:
	docker build --no-cache -t $(IMAGE_NAME):$(IMAGE_TAG) .

run:
	docker run -it --rm -v `pwd`:/host $(IMAGE_NAME):$(IMAGE_TAG)

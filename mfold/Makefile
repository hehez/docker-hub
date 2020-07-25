# HELP
# This will output the help for each task
# thanks to https://marmelab.com/blog/2016/02/29/auto-documented-makefile.html
.PHONY: help
.SILENT:

help: ## This help.
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

.DEFAULT_GOAL := help

CONTAINER_NAME=mfold
IMG_NAME=hehez/mfold:1.0
# IMG_NAME=mfold-img

# DOCKER TASKS
# Build the container
build: ## Build an image from Dockerfile
	docker build -t $(IMG_NAME) .

build-nc: ## Build an image without caching
	docker build --no-cache -t $(IMG_NAME) .

prune: ## Clean all that is not actively used
	docker system prune -af

stop: ## Stop and remove a running container
	docker stop $(CONTAINER_NAME); docker rm $(CONTAINER_NAME)

clean: ## Stop and remove ALL containers
	docker stop $$(docker ps -a -q); docker rm $$(docker ps -a -q) 

# Test example test.fasta
test: ## Run mfold with given example -- test.fasta
	docker run --rm -v $(PWD)/example:/data $(IMG_NAME) sh -c 'mfold SEQ=test.fasta' 

# Operation
run: ## Run container in detached mode (background)
	docker run -d -it --name $(CONTAINER_NAME) \
	-v $(PWD)/input:/data/input \
	-v $(PWD)/output:/data/output \
	$(IMG_NAME)

login: ## Attach the running container, manually run commands inside container
	docker exec -it $(CONTAINER_NAME) sh

mfold: ## Run mfold with fasta file in input directory. i.e. make mfold SEQ=test.fasta
	docker run --rm \
	-v $(PWD)/input:/data/input \
	-v $(PWD)/output:/data/output \
	$(IMG_NAME) sh -c 'cd output; mfold SEQ=/data/input/$(name)'

# TODO: may add more commands

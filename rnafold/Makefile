# HELP
# This will output the help for each task
# thanks to https://marmelab.com/blog/2016/02/29/auto-documented-makefile.html
.PHONY: help

# No verbose output
.SILENT:

help: ## This help.
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

.DEFAULT_GOAL := help

CONTAINER_NAME=rnafold
IMG_NAME=rnafold-img

# DOCKER TASKS
# Build the container
build: ## Build an image from Dockerfile (Optimized Image)
	docker build -t $(IMG_NAME) .

build-nc: ## Build an image without caching (Optimized Image)
	docker build --no-cache -t $(IMG_NAME) .

build-whole: ## Build an image from Dockerfile-whole
	docker build -t $(IMG_NAME) -f Dockerfile-whole .

build-w-nc: ## Build an image without caching (whole)
	docker build --no-cache -t $(IMG_NAME) -f Dockerfile-whole .

prune: ## Clean all that is not actively used
	docker system prune -af

stop: ## Stop and remove a running container
	docker stop $(CONTAINER_NAME); docker rm $(CONTAINER_NAME)

clean: ## Stop and remove ALL containers
	docker stop $$(docker ps -a -q); docker rm $$(docker ps -a -q) 

# Test example test.fasta
test: ## Run RNAfold with given example -- test.fasta
	docker run --rm -v $(PWD)/example:/data $(IMG_NAME) sh -c 'RNAfold < /data/test.fasta' 

# Operation
run: ## Run container in detached mode (background)
	# docker run -d -it --name $(CONTAINER_NAME) -v $(PWD)/example:/data $(IMG_NAME)
	docker run -d -it --name $(CONTAINER_NAME) \
	-v $(PWD)/input:/data/input \
	-v $(PWD)/output:/data/output \
	$(IMG_NAME)

login: ## Attach the running container, manually run commands inside container
	docker exec -it $(CONTAINER_NAME) sh

rnafold: ## Run RNAfold with fasta file in input directory. i.e. make rnafold name=test.fasta
	docker run --rm \
	-v $(PWD)/input:/data/input \
	-v $(PWD)/output:/data/output \
	$(IMG_NAME) sh -c 'RNAfold < /data/input/$(name) | tee output/$(name).out.txt'

# TODO: may add more commands

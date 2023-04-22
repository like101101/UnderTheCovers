BUILT_IMAGE = $(shell make -C ../.. show-tag)
CWD := $(shell pwd)
CONTAINER_DIR := /home/jovyan

ASSIGNMENT_BUILT_DIRS := PS1B PS4B

pull: ## pull most recent public version
	docker pull $(BUILT_IMAGE)

build:
	@for dir in $(ASSIGNMENT_BUILT_DIRS); do \
        $(MAKE) -C $$dir; \
    done

ibuild: MOUNT = $(CWD):$(CONTAINER_DIR)
ibuild: 
	docker run -u 0 -v $(MOUNT) $(BUILT_IMAGE) make build

itest: MOUNT = $(CWD):$(CONTAINER_DIR)
itest: ibuild
	docker run -u 0 -v $(MOUNT) $(BUILT_IMAGE) ./testassignments.sh

run: MOUNT = $(CWD):$(CONTAINER_DIR)
run:
	docker run --privileged -it --rm -u 0 -v $(MOUNT) $(BUILT_IMAGE) /bin/bash

test: build
	./testassignments.sh

clean: 
	@for dir in $(ASSIGNMENT_BUILT_DIRS); do \
        $(MAKE) -C $$dir clean; \
    done



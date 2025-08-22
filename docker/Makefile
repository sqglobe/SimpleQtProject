CURR_DIR=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

# Setup the folder for the build artifacts
RELEASE_DIR=$(CURR_DIR)/releases

# List the name of docker files which might be used for product building
DOCKERS=ubuntu-bionic ubuntu-noble windows

# Construct folder for build artifacts
$(shell   mkdir -p $(RELEASE_DIR))

# By default build product with each container
all: $(DOCKERS)

# Build docker image and run the product compilation
# Logic about how to compile is encoded into particular
# docker image
%: %.docker
	docker build -t  simple-qt-$(strip $(subst .docker,, $< )) --file $< . 
	docker run --mount type=bind,source=$(RELEASE_DIR),target=/app/res --mount type=bind,source=$(CURR_DIR)/../,target=/app/src simple-qt-$(strip $(subst .docker,, $< ))	
	
clean:
	rm -Rf $(RELEASE_DIR)


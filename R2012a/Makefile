ISO_IMAGE ?= R2012a_UNIX.iso
MOUNT_DIR ?= iso/
DOCKER ?= sudo docker
BUILDER ?= sudo DOCKER_BUILDKIT=1 BUILDKIT_PROGRESS=plain docker build
TAG ?= R2012a
IMAGE ?= slaclab/matlab
MATLAB_INSTALL_KEY ?= TBD
IMAGE_PATH ?= /sdf/sw/images/matlab/
CACHE ?= 

mount:
	mkdir -p $(MOUNT_DIR)
	sudo mount -o loop $(ISO_IMAGE) $(MOUNT_DIR)

unmount:
	sudo umount $(MOUNT_DIR)
	rm -rf $(MOUNT_DIR)

build:
	$(BUILDER) --build-arg MATLAB_INSTALL_KEY=$(MATLAB_INSTALL_KEY) $(CACHE) . -t $(IMAGE):$(TAG)

push:
	$(DOCKER) push $(IMAGE):$(TAG)

singularity:
	mkdir -p $(IMAGE_PATH)/$(TAG)/
	singularity pull -F $(IMAGE_PATH)/$(TAG)/matlab@$(TAG).sif docker://$(IMAGE):$(TAG)

	

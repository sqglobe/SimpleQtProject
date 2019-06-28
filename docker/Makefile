CURR_DIR=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

RELEASE_DIR=$(CURR_DIR)/releases

IMG_DIR=$(CURR_DIR)/img/

DOCKERS=centos7 ubuntu-bionic ubuntu-xenial

$(shell   mkdir -p $(IMG_DIR))
$(shell   mkdir -p $(RELEASE_DIR))


# чтобы не удалялись промежуточные файлы
.SECONDARY: $(addprefix $(IMG_DIR),$(addsuffix .image,$(DOCKERS)) )

all: $(DOCKERS)

%: $(addprefix $(IMG_DIR), %.image)
	docker run --mount type=bind,source=$(RELEASE_DIR),target=/app/res secure-dialogues-$(strip $(subst .image,, $(notdir $<) ))

$(addprefix $(IMG_DIR), %.image): %.docker
	docker build -t  secure-dialogues-$(strip $(subst .docker,, $< )) --file $< . 
	$(file > $@, "ON")
	
	
clean:
	rm -Rf $(IMG_DIR)
	rm -Rf $(RELEASE_DIR)


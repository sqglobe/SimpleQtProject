CURR_DIR=$(shell dirname $(realpath $(lastword $(MAKEFILE_LIST))))

# определяем папку для копирования артефактов сборки
RELEASE_DIR=$(CURR_DIR)/releases

# задаем список систем, для которых выполняется сборка
DOCKERS=centos7 ubuntu-bionic ubuntu-xenial

# создаем необходмую дирректорию
$(shell   mkdir -p $(RELEASE_DIR))

# по умолчанию запускаем сборку для всех
all: $(DOCKERS)

# сборка для контретной системы включаем создание образа и запуск контейнера
%: %.docker
	docker build -t  simple-qt-$(strip $(subst .docker,, $< )) --file $< . 
	docker run --mount type=bind,source=$(RELEASE_DIR),target=/app/res simple-qt-$(strip $(subst .docker,, $< ))	
	
clean:
	rm -Rf $(RELEASE_DIR)


all:
	echo 'Nothing to do' && exit 1
.PHONY: all

clean-dist:
	rm -rf ./dist
.PHONY: clean-dist

clean-all: clean-dist
	rm -rf ./build
.PHONY: clean-all

fetch-crashpad:
	bash ./fetch.sh
.PHONY: fetch-crashpad

build-shell:
	bash ./build-shell.sh
.PHONY: build-shell

collect:
	bash ./collect-files.sh
.PHONY: collect

build-docker:
	bash ./build-docker.sh
.PHONY: build-docker

collect-windows:
	bash collect-files-windows.sh
.PHONY: collect-windows

build-windows-all: clean-all fetch-crashpad build-shell collect-windows
.PHONY: build-windows-all

build-linux-all: clean-all fetch-crashpad build-docker
	sudo chown -R $(USER) ./build
	$(MAKE) collect
.PHONY: build-linux-all

build-mac-all: clean-all fetch-crashpad build-shell collect
.PHONY: build-mac-all

generate-getsentry-patch:
	rm -rf .crashpad-getsentry
	git clone --branch getsentry https://github.com/getsentry/crashpad .crashpad-getsentry
	cd .crashpad-getsentry \
		&& git fetch origin master \
		&& git format-patch --stdout origin/master...HEAD > ../patches/getsentry.patch
.PHONY: generate-getsentry-patch

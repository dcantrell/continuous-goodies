# Simple driver when using meson for a project.  Implements
# common Makefile targets as well as 'release', 'srpm', and 'koji'

MESON_BUILD_DIR = build
topdir := $(shell realpath $(dir $(lastword $(MAKEFILE_LIST))))

all: setup
	ninja -C build -v

setup:
	meson setup $(MESON_BUILD_DIR)

check: setup
	meson test -C build -v

srpm:
	$(topdir)/utils/srpm.sh

release:
	$(topdir)/utils/release.sh -A

koji: srpm
	$(topdir)/utils/submit-koji-builds.sh $$(ls -1 $(topdir)/*.tar.*) $$(basename $(topdir))

clean:
	-rm -rf $(MESON_BUILD_DIR)

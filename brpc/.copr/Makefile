TOP = $(realpath $(dir $(lastword $(MAKEFILE_LIST))))

# Version
MAJOR=0
MINOR=9
PATCH=7
RELEASE=1

RPMTOPDIR=$(TOP)/rpmbuild
SOURCEDIR=$(RPMTOPDIR)/SOURCES
SPECDIR=$(RPMTOPDIR)/SPECS
SPECFILE=$(SPECDIR)/vespa-brpc.spec

srpm:
	dnf install -y rpmdevtools
	mkdir -p $(SPECDIR) $(SOURCEDIR)
	cat vespa-brpc.spec.tmpl | sed "s/_TMPL_VER_MAJOR/$(MAJOR)/" | sed "s/_TMPL_VER_MINOR/$(MINOR)/" | sed "s/_TMPL_VER_PATCH/$(PATCH)/" | sed "s/_TMPL_VER_RELEASE/$(RELEASE)/" > $(SPECFILE)
	spectool -g -C $(SOURCEDIR) $(SPECFILE)
	rpmbuild -bs --define "_topdir $(RPMTOPDIR)" $(SPECFILE)
	cp -a $(RPMTOPDIR)/SRPMS/* $(outdir)
clean:
	-rm -rf $(RPMTOPDIR)

.PHONY: srpm clean

#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2011, 2013, Oracle and/or its affiliates. All rights reserved.
#

include ../../make-rules/shared-macros.mk

COMPONENT_NAME=		ircii
COMPONENT_VERSION=	20111115
IPS_COMPONENT_VERSION=  0.2011.11.15
COMPONENT_PROJECT_URL=	http://www.eterna.com.au/ircii/
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:629a0a335c790aa5fa9f327532d1d45fd37d2fcd1902e8b0ee28b51994dcf604
COMPONENT_ARCHIVE_URL=	ftp://ircii.warped.com/pub/ircII/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	utility/ircii

include ../../make-rules/prep.mk
include ../../make-rules/configure.mk
include ../../make-rules/ips.mk

CONFIGURE_ENV += CC="$(CC)"

# We need to reset configure options here because ircii is confused with
# CC and CFLAGS definitions as configure parameters.
CONFIGURE_OPTIONS       = --prefix=/usr
CONFIGURE_OPTIONS       += --mandir=$(CONFIGURE_MANDIR)
CONFIGURE_OPTIONS       += --bindir=$(CONFIGURE_BINDIR.$(BITS))
CONFIGURE_OPTIONS       += $(CONFIGURE_OPTIONS.$(BITS))

# The ircio and wserv are now installed in the libexecdir, which by
# default is /usr/libexec. We want to install them under /usr/bin.
# One would think that you could just set --libexecdir=/usr/bin but no.
# The configure script has some logic that just blindly resets it back
# to /usr/libexec. This problem has been reported to the ircii maintainer.
#
# This action modifies the libexecdir setting in the Makefile to /usr/bin
COMPONENT_POST_CONFIGURE_ACTION = \
	$(GSED) -i -e 's|/usr/libexec|/usr/bin|' $(BUILD_DIR_32)/Makefile

# Enable ASLR for this component
ASLR_MODE = $(ASLR_ENABLE)

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:           $(NO_TESTS)

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

include ../../make-rules/depend.mk

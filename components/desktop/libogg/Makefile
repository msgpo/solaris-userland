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
# Copyright (c) 2016, 2017, Oracle and/or its affiliates. All rights reserved.
#

BUILD_BITS= 		32_and_64
COMPILER=		gcc
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		libogg
COMPONENT_VERSION=	1.2.2
COMPONENT_PROJECT_URL=	https://xiph.org/ogg/
COMPONENT_ARCHIVE_HASH= \
	sha256:ab000574bc26d5f01284f5b0f50e12dc761d035c429f2e9c70cb2a9487d8cfba
COMPONENT_ARCHIVE_URL=	http://downloads.xiph.org/releases/ogg/$(COMPONENT_ARCHIVE)
COMPONENT_BUGDB=	gnome/multimedia
COMPONENT_ANITYA_ID=	1694

TPNO=			9571

TEST_TARGET = $(NO_TESTS)

# ogg-vorbis is not unlockable in S11 gnome-incorporation
include $(WS_MAKE_RULES)/no-evaluation.mk

include $(WS_MAKE_RULES)/common.mk

CONFIGURE_ENV += PATH="$(GNUBIN):$(PATH)"

ifneq ($(BUILD_TYPE), evaluation)
# Merge 32-bit & 64-bit versions of config_types.h 
install: $(BUILD_DIR)/.merged-header

$(BUILD_DIR)/.merged-header: $(BUILD_DIR_32)/.installed $(BUILD_DIR_64)/.installed
	-$(RM) $(PROTO_DIR)/include/ogg/config_types.h
	$(GDIFF) -D _LP64 \
	    $(BUILD_DIR_32)/include/ogg/config_types.h $(BUILD_DIR_64)/include/ogg/config_types.h \
	    > $(PROTO_DIR)/usr/include/ogg/config_types.h; \
	diffstatus=$$? ; \
	if (( $$diffstatus != 1 )) ; then exit $$diffstatus ; fi
endif

REQUIRED_PACKAGES += system/library/math

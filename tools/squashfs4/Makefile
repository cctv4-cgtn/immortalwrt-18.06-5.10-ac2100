#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=squashfs4
PKG_CPE_ID:=cpe:/a:phillip_lougher:squashfs
PKG_VERSION:=4.7.4
PKG_RELEASE=2

PKG_SOURCE:=squashfs-tools-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/plougher/squashfs-tools/releases/download/$(PKG_VERSION)/
PKG_HASH:=91c49f9a1ed972ad00688a38222119e2baf49ba74cf5fda05729a79d7d59d335

HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/host-build.mk

define Host/Compile
	+$(HOST_MAKE_VARS) \
	$(MAKE) $(HOST_JOBS) -C $(HOST_BUILD_DIR)/squashfs-tools \
		LZ4_SUPPORT=0 \
		LZO_SUPPORT=0 \
		ZSTD_SUPPORT=1 \
		GZIP_SUPPORT=1 \
		XZ_SUPPORT=1 \
		LZMA_XZ_SUPPORT=1 \
		XZ_EXTENDED_OPTIONS=1 \
		EXTRA_CFLAGS="-I$(STAGING_DIR_HOST)/include" \
		mksquashfs unsquashfs
endef

define Host/Install
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/squashfs-tools/mksquashfs $(STAGING_DIR_HOST)/bin/mksquashfs4
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/squashfs-tools/unsquashfs $(STAGING_DIR_HOST)/bin/unsquashfs4
endef

define Host/Clean
	rm -f $(STAGING_DIR_HOST)/bin/mksquashfs4
	rm -f $(STAGING_DIR_HOST)/bin/unsquashfs4
endef

$(eval $(call HostBuild))

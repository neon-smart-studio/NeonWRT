#
# Copyright (C) 2006-2015 OpenWrt.org
# Copyright (C) 2015-2017 Christian Beier <dontmind@freeshell.org>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ola
PKG_VERSION:=0.10.9
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/OpenLightingProject/ola
PKG_MIRROR_HASH:=55b9c82dec4133c3895a9af99a3245764ece14fc5b0a4e0841686903b1d6f365

PKG_MAINTAINER:=Christian Beier <dontmind@freeshell.org>
PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

HOST_BUILD_DEPENDS:=protobuf/host
PKG_BUILD_DEPENDS:=ola/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/ola
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Open Lighting Architecture Daemon
  URL:=https://www.openlighting.org/
  DEPENDS:=+protobuf +libftdi1 +libusb-1.0 +libuuid +libstdcpp +libpthread +librt +zlib +libncurses +liblo +libmicrohttpd
endef

define Package/ola/description
  OLA (Open Lighting Architecture) is a framework that allows applications to
  send and receive DMX512, using various hardware devices and 'DMX over IP'
  protocols. It enables software controllers talk to DMX hardware.
endef

CONFIGURE_ARGS += \
	--disable-dependency-tracking \
	--disable-static \
	--disable-fatal-warnings \
	--disable-unittests \
	--without-dns-sd \
	--with-ola-protoc-plugin="$(STAGING_DIR_HOSTPKG)/bin/ola_protoc_plugin"

HOST_CONFIGURE_ARGS += \
	--disable-all-plugins \
	--disable-osc \
	--disable-uart \
	--disable-libusb \
	--disable-http  \
	--disable-examples \
	--disable-unittests \
	--disable-doxygen-html \
	--disable-doxygen-doc \
	--with-protoc=$(STAGING_DIR_HOSTPKG)/bin/protoc

# only build the ola_protoc thingy
define Host/Compile
	cd $(HOST_BUILD_DIR); \
		$(MAKE) protoc/ola_protoc_plugin
endef

define Host/Install
	$(INSTALL_DIR) $(STAGING_DIR_HOSTPKG)/bin
	$(CP) $(HOST_BUILD_DIR)/protoc/ola_protoc_plugin $(STAGING_DIR_HOSTPKG)/bin
endef


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ola $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/olad $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

define Package/ola/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/olad.init $(1)/etc/init.d/olad

	$(INSTALL_DIR) $(1)/usr/share/ola/pids
	$(CP) $(PKG_INSTALL_DIR)/usr/share/ola/pids/* $(1)/usr/share/ola/pids

	$(INSTALL_DIR) $(1)/usr/share/olad/www
	$(CP) $(PKG_INSTALL_DIR)/usr/share/olad/www/* $(1)/usr/share/olad/www
endef

define Package/ola/postinst
#!/bin/sh

# make sure the conf dir exists and is writeable by the group olad uses
mkdir -p $${IPKG_INSTROOT}/etc/ola
chgrp nogroup $${IPKG_INSTROOT}/etc/ola
chmod 775 $${IPKG_INSTROOT}/etc/ola
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,ola))

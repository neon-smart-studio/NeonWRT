#
# Copyright (C) 2008-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=radsecproxy
PKG_VERSION:=1.9.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/radsecproxy/radsecproxy/releases/download/$(PKG_VERSION)/
PKG_HASH:=e08e4e04d188deafd0b55b2f66b1e7fff9bdb553fb170846590317d02c9dc5db

PKG_MAINTAINER:=Toke Høiland-Jørgensen <toke@toke.dk>
PKG_LICENSE:=BSD-3-CLAUSE
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:uninett:radsecproxy

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/radsecproxy
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl +libpthread +libnettle
  TITLE:=radsecproxy
  URL:=https://radsecproxy.github.io/
endef

define Package/radsecproxy/description
  A generic radius proxy for UDP/TLS (RadSec)
endef

CONFIGURE_ARGS+= \
	--with-ssl="$(STAGING_DIR)/usr"

define Package/radsecproxy/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/radsecproxy $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_DATA) ./files/radsecproxy.conf $(1)/etc/config/radsecproxy
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/radsecproxy.init $(1)/etc/init.d/radsecproxy
endef

define Package/radsecproxy/conffiles
/etc/config/radsecproxy
endef

$(eval $(call BuildPackage,radsecproxy))


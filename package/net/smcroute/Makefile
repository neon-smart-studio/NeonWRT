#
# Copyright (C) 2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=smcroute
PKG_VERSION:=2.5.6
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/troglobit/smcroute/releases/download/$(PKG_VERSION)
PKG_HASH:=0be38f617e322daafaa941c02423239f5c117b940cf0f45bacadb6733c4b3916

include $(INCLUDE_DIR)/package.mk

define Package/smcroute
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Routing and Redirection
	TITLE:=Static Multicast Routing Daemon
	URL:=http://troglobit.com/smcroute.html
	MAINTAINER:=Moritz Warning <moritzwarning@web.de>
endef

define Package/smcroute/description
	SMCRoute is a command line tool to manipulate the multicast routes of the Linux kernel.
endef

define Package/smcroute/conffiles
/etc/smcroute.conf
endef

CONFIGURE_ARGS += \
	--without-libcap

define Package/smcroute/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/smcrouted $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/smcroutectl $(1)/usr/bin/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/smcroute.conf $(1)/etc
	$(INSTALL_BIN) ./files/smcroute.init $(1)/etc/init.d/smcroute
endef

$(eval $(call BuildPackage,smcroute))

#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ser2net
PKG_VERSION:=4.6.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/ser2net
PKG_HASH:=63bafcd65bb9270a93b7d5cdde58ccf4d279603ff6d044ac4b484a257cda82ce

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Michael Heimpold <mhei@heimpold.de>

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

CONFIGURE_ARGS += \
	--with-pam=no \
	--with-pthreads \
	--with-sysfs-led-support

define Package/ser2net
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Serial to Network Proxy
  URL:=https://sourceforge.net/projects/ser2net/
  DEPENDS:=+libgensio +libyaml +libpthread
endef

define Package/ser2net/description
  This project provides a proxy that allows telnet/tcp connections to be made to
  serial ports on a machine.
endef

define Package/ser2net/conffiles
/etc/config/ser2net
/etc/ser2net.yaml
endef

define Package/ser2net/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/ser2net $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/ser2net.yaml $(1)/etc/

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/ser2net.config $(1)/etc/config/ser2net

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/ser2net.init $(1)/etc/init.d/ser2net
endef

$(eval $(call BuildPackage,ser2net))

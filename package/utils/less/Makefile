#
# Copyright (C) 2010-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=less
PKG_VERSION:=661
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:= @GNU/less \
	http://www.greenwoodsoftware.com/less
PKG_HASH:=2b5f0167216e3ef0ffcb0c31c374e287eb035e4e223d5dae315c2783b6e738ed

PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Julen Landa Alustiza <julen@zokormazo.info>
PKG_CPE_ID:=cpe:/a:gnu:less

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/less
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Pager program similar to more
  URL:=http://www.greenwoodsoftware.com/less/
  ALTERNATIVES:=200:/usr/bin/less:/usr/libexec/less-gnu
  DEPENDS:=+libncursesw
  PROVIDES:=less-wide
endef

define Package/less/description
  Full version of GNU less utility
endef

define Package/less/install
	$(INSTALL_DIR) $(1)/usr/libexec
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/less $(1)/usr/libexec/less-gnu
endef

$(eval $(call BuildPackage,less))

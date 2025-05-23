#
# Copyright (C) 2009-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pcsc-lite
PKG_VERSION:=2.2.3
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://pcsclite.apdu.fr/files/
PKG_HASH:=cab1e62755713f62ce1b567954dbb0e9a7e668ffbc3bbad3ce85c53f8f4e00a4
PKG_MAINTAINER:=Daniel Golle <daniel@makrotopia.org>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:muscle:pcsc-lite

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/pcsc-lite/Default
  TITLE:=Access a smart card using SCard API (PC/SC)
  URL:=https://pcsclite.apdu.fr/
endef

define Package/pcsc-lite/Default/description
  The purpose of PC/SC Lite is to provide a Windows(R) SCard
  interface in a very small form factor for communicating to
  smart cards and smart cards readers.
endef

define Package/libpcsclite
  $(call Package/pcsc-lite/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+= (library)
  DEPENDS:=+libusb-1.0 +libpthread +librt
endef

define Package/libpcsclite/description
  $(call Package/pcsc-lite/Default/description)
  .
  This package contains the PC/SC shared library.
endef

define Package/pcscd
  $(call Package/pcsc-lite/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE+= (daemon)
  DEPENDS:=+libpcsclite
endef

define Package/pcscd/description
  $(call Package/pcsc-lite/Default/description)
  .
  This package contains the PC/SC daemon.
endef

TARGET_CFLAGS += $(FPIC)
TARGET_LDFLAGS += -lpthread

MESON_ARGS += \
	-Dlibudev=false \
	-Dlibsystemd=false \
	-Dlibusb=true \
	-Dpolkit=false \
	-Dipcdir='/var/run/pcscd' \
	-Dusbdropdir='/usr/lib/pcsc/drivers'

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/PCSC
	$(CP) $(PKG_INSTALL_DIR)/usr/include/PCSC/* $(1)/usr/include/PCSC/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpcsclite.{a,so*} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpcsclite_real.{a,so*} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libpcsclite.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libpcsclite/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpcsclite.so.* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpcsclite_real.so.* $(1)/usr/lib/
endef

define Package/pcscd/conffiles
/etc/reader.conf.d/reader.conf
endef

define Package/pcscd/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/pcscd $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/pcscd.init $(1)/etc/init.d/pcscd
	$(INSTALL_DIR) $(1)/etc/reader.conf.d
endef

$(eval $(call BuildPackage,libpcsclite))
$(eval $(call BuildPackage,pcscd))

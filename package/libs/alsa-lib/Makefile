#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=alsa-lib
PKG_VERSION:=1.2.11
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://www.alsa-project.org/files/pub/lib/ \
		https://distfiles.gentoo.org/distfiles/
PKG_HASH:=9f3f2f69b995f9ad37359072fbc69a3a88bfba081fc83e9be30e14662795bb4d

PKG_MAINTAINER:=Ted Hess <thess@kitschensync.net>, \
		Peter Wagner <tripolar@gmx.at>

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16 no-lto

include $(INCLUDE_DIR)/package.mk

define Package/alsa-lib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=ALSA (Advanced Linux Sound Architecture) library
  URL:=https://www.alsa-project.org/
  DEPENDS:=@AUDIO_SUPPORT +kmod-sound-core +libpthread +librt
  LICENSE:=LGPL-2.1-or-later
  LICENSE_FILES:=COPYING
endef

define Package/alsa-lib/description
 This is the library package for alsa, needed by some userspace programs.
 You must have enabled the ALSA support in the kernel.
endef

define Package/aserver
  SECTION:=sound
  CATEGORY:=Sound
  TITLE:=ALSA (Advanced Linux Sound Architecture) server
  URL:=https://www.alsa-project.org/
  DEPENDS:=+alsa-lib
  LICENSE:=GPL-2.0-or-later
  LICENSE_FILES:=aserver/COPYING
endef

define Package/aserver/description
 This is the aserver application for ALSA.
endef

define Package/alsa-lib/conffiles
/etc/asound.conf
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS+= \
		--disable-python \
		--disable-debug \
		--without-debug \
		--without-versioned \
		$(SOFT_FLOAT_CONFIG_OPTION)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/alsa \
		$(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libasound.{la,so*} \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libatopology.{la,so*} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/alsa.pc \
		$(1)/usr/lib/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/share/aclocal
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/aclocal/alsa.m4 \
		$(1)/usr/share/aclocal/
endef

define Package/alsa-lib/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libasound.so.* \
		$(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libatopology.so.* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/share/alsa/{cards,ctl,pcm}
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/alsa/alsa.conf \
		$(1)/usr/share/alsa/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/alsa/ctl/* \
		$(1)/usr/share/alsa/ctl/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/alsa/pcm/* \
		$(1)/usr/share/alsa/pcm/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/share/alsa/cards/* \
		$(1)/usr/share/alsa/cards/
endef

define Package/aserver/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/aserver $(1)/usr/bin
endef

$(eval $(call BuildPackage,alsa-lib))
$(eval $(call BuildPackage,aserver))

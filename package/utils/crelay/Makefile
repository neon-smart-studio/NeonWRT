#
# Copyright (C) 2015-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=crelay
PKG_VERSION:=0.14.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/ondrej1024/crelay/tar.gz/V$(PKG_VERSION)?
PKG_HASH:=291f51d60c3003ad594ac2c10f75b0c5d0b40e49b298f73caf6a47afe3279fde

PKG_MAINTAINER:=Ted Hess <thess@kitschensync.net>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/meson.mk

define Package/crelay
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=USB relay remote control daemon
  URL:=https://github.com/ondrej1024/crelay
  DEPENDS:=+libftdi1 +hidapi +libusb-1.0
endef

define Package/crelay/description
 crelay is used to control different relay cards in a unified manner. It provides
 several interfaces for controlling the relays locally or remotely by a web browser
 or a smartphone.  The card which is detected first will be used. A WebUI control is
 available on port 8000 (default)
 .
 Currently supported relay cards:
      - Conrad USB 4-channel relay card
      - Sainsmart USB 4/8-channel relay board
      - Sainsmart USB 16-channel relay control module
      - Generic GPIO relays
      - HID API compatible relay card
endef

define Package/crelay/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/crelay $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/crelay.init $(1)/etc/init.d/crelay
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/conf/crelay.conf $(1)/etc
endef

$(eval $(call BuildPackage,crelay))

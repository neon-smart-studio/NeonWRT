#
# Copyright (C) 2022 Oleg Derevenetz <oleg.derevenetz@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bwping
PKG_VERSION:=2.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/bwping
PKG_HASH:=1d8762227f40909f6d42ef756ebc2c258e5fd4f268ff63ecc544b8d6f0802c82

PKG_MAINTAINER:=Oleg Derevenetz <oleg.derevenetz@gmail.com>
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/bwping
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Tool to measure bandwidth and RTT between two hosts using ICMP
  URL:=https://bwping.sourceforge.io/
endef

define Package/bwping/description
  BWPing is a tool to measure bandwidth and response times between two
  hosts using Internet Control Message Protocol (ICMP) echo request/echo
  reply mechanism. It does not require any special software on the remote
  host. The only requirement is the ability to respond on ICMP echo request
  messages. BWPing supports both IPv4 and IPv6 networks.
endef

define Package/bwping/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/$(PKG_NAME) $(1)/usr/sbin/
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/$(PKG_NAME)6 $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,bwping))

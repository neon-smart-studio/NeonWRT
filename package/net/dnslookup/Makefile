# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=dnslookup
PKG_VERSION:=1.11.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/ameshkov/dnslookup/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=31967c89406aa6da5f69c563815e58478b530c8e55f0d995065a363f68d5e535

PKG_MAINTAINER:=Tianling Shen <cnsztl@immortalwrt.org>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/ameshkov/dnslookup
GO_PKG_LDFLAGS_X:=main.VersionString=v$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include ../../lang/golang/golang-package.mk

define Package/dnslookup
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=Simple command line utility to make DNS lookups to the specified server
  URL:=https://github.com/ameshkov/dnslookup
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle
endef

define Package/dnslookup/description
  Simple command line utility to make DNS lookups.
  Supports all known DNS protocols: plain DNS, DoH, DoT, DoQ, DNSCrypt.
endef

$(eval $(call GoBinPackage,dnslookup))
$(eval $(call BuildPackage,dnslookup))

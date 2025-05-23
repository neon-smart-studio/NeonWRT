# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023 Jonas Jelonek

include $(TOPDIR)/rules.mk

PKG_NAME:=croc
PKG_VERSION:=10.2.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/schollz/croc/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=78bf0efd00daa9002bcdeb460f4ddaf82dde4480e63862feab0958ed9ed54963

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Jonas Jelonek <jelonek.jonas@gmail.com>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/schollz/croc/v10
GO_PKG_BUILD_PKG:=$(GO_PKG)
GO_PKG_LDFLAGS_X:=$(GO_PKG)/src/cli.Version=v$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include ../../lang/golang/golang-package.mk

define Package/croc
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=File Transfer
  TITLE:=Easily and securely send things from one computer to another
  URL:=https://github.com/schollz/croc
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/croc/description
  croc is a tool that allows any two computers to simply and securely
  transfer files and folders by using a relay.
endef

$(eval $(call GoBinPackage,croc))
$(eval $(call BuildPackage,croc))

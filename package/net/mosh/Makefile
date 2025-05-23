#
# Copyright (C) 2011-2013 Entware
# Copyright (C) 2018 Jakub Tymejczyk <jakub.tymejczyk.pl>
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mosh
PKG_VERSION:=1.4.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://mosh.org/
PKG_HASH:=872e4b134e5df29c8933dff12350785054d2fd2839b5ae6b5587b14db1465ddd

PKG_MAINTAINER:=Rosen Penev <rosenp@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=protobuf/host
PKG_BUILD_FLAGS:=gc-sections lto

include $(INCLUDE_DIR)/package.mk

define Package/mosh/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=SSH
  TITLE:=Mosh mobile shell
  DEPENDS:=+libncursesw +libopenssl +protobuf
  URL:=https://mosh.org/
endef

define Package/mosh-client
$(call Package/mosh/Default)
 TITLE+= (client)
endef

define Package/mosh-server
$(call Package/mosh/Default)
 TITLE+= (server)
endef

define Package/mosh-full
$(call Package/mosh/Default)
 TITLE+= (full)
 DEPENDS:= \
    +mosh-client \
    +mosh-server \
    +perlbase-autoloader \
    +perlbase-config \
    +perlbase-errno \
    +perlbase-essential \
    +perlbase-fcntl \
    +perlbase-getopt \
    +perlbase-io \
    +perlbase-posix \
    +perlbase-selectsaver \
    +perlbase-socket \
    +perlbase-symbol \
    +perlbase-text \
    +perlbase-tie \
    +perlbase-xsloader
endef


define Package/mosh/Default/description
 Mosh is a remote terminal application that allows roaming, supports
 intermittent connectivity, and provides intelligent local echo and line
 editing of user keystrokes.
endef

define Package/mosh-client/description
$(call Package/mosh/Default/description)
 This is a mosh client.
endef

define Package/mosh-server/description
$(call Package/mosh/Default/description)
 This is a mosh server.
endef

define Package/mosh-full/description
$(call Package/mosh/Default/description)
 This is a full package with perl wrapper script
endef

CONFIGURE_ARGS += \
	--disable-compile-warnings \
	--disable-hardening \
	--without-utempter

CONFIGURE_VARS += \
	ac_cv_have_decl_ffs=yes

TARGET_CXXFLAGS += -std=c++11
TARGET_LDFLAGS += -lncurses

define Package/mosh-client/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mosh-client $(1)/usr/bin/
endef

define Package/mosh-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mosh-server $(1)/usr/bin/
endef

define Package/mosh-full/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mosh $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mosh-client))
$(eval $(call BuildPackage,mosh-server))
$(eval $(call BuildPackage,mosh-full))

#
# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=uacme
PKG_VERSION:=1.7.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/ndilieto/uacme/tar.gz/upstream/$(PKG_VERSION)?
PKG_HASH:=a638fe0878dba8fdda62f89e7a284243edbcd31b92c11b5cfdc7d3efd9547bca

PKG_MAINTAINER:=Lucian Cristian <lucian.cristian@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-upstream-$(PKG_VERSION)
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_CONFIG_DEPENDS:= \
  CONFIG_LIBCURL_GNUTLS \
  CONFIG_LIBCURL_MBEDTLS \
  CONFIG_LIBCURL_OPENSSL \
  CONFIG_LIBCURL_WOLFSSL \
  CONFIG_LIBCURL_NOSSL \
  CONFIG_UACME_UALPN

include $(INCLUDE_DIR)/package.mk


define Package/uacme/Default
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+uacme
  TITLE:=lightweight client for ACMEv2
  URL:=https://github.com/ndilieto/uacme
endef

define Package/uacme
  $(call Package/uacme/Default)
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libcurl +LIBCURL_WOLFSSL:libmbedtls
  TITLE:=lightweight client for ACMEv2
  Menu:=1
endef

define Package/uacme-ualpn
  $(call Package/uacme/Default)
  DEPENDS:=+uacme +PACKAGE_uacme-ualpn:libev
  TITLE:=ualpn for uacme
  URL:=https://github.com/ndilieto/uacme
endef

define Package/uacme/Default/description
  lightweight client for the RFC8555 ACMEv2 protocol, written in plain C code
  with minimal dependencies (libcurl and one of GnuTLS, OpenSSL or mbedTLS).
  The ACMEv2 protocol allows a Certificate Authority (https://letsencrypt.org
  is a popular one) and an applicant to automate the process of verification
  and certificate issuance. The protocol also provides facilities for other
  certificate management functions, such as certificate revocation.
endef

define Package/uacme/config
if PACKAGE_uacme && LIBCURL_WOLFSSL
  comment "libcurl uses WolfSSL; uacme will install mbedtls"
  comment "Choose another SSL lib in libcurl to avoid this"
endif
if PACKAGE_uacme && LIBCURL_NOSSL
  comment "libcurl is built without ssl; uacme needs ssl support"
  comment "Choose another SSL lib in libcurl to avoid this"
endif
if PACKAGE_uacme && LIBCURL_MBEDTLS
  comment "uacme will install mbedtls"
endif
endef
TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

CONFIGURE_ARGS+= \
	--disable-maintainer-mode \
	--disable-docs \
	$(if $(CONFIG_PACKAGE_uacme-ualpn),--with-ualpn,--without-ualpn) \
	$(if $(CONFIG_LIBCURL_GNUTLS),--with-gnutls --without-mbedtls --without-openssl,) \
	$(if $(CONFIG_LIBCURL_MBEDTLS),--without-gnutls --with-mbedtls --without-openssl,) \
	$(if $(CONFIG_LIBCURL_OPENSSL),--without-gnutls --without-mbedtls --with-openssl,) \
	$(if $(CONFIG_LIBCURL_WOLFSSL),--without-gnutls --with-mbedtls --without-openssl,)

define Package/uacme/conffiles
/etc/config/acme
/etc/acme
endef

define Package/uacme/install
	$(INSTALL_DIR) \
	 $(1)/usr/sbin \
	 $(1)/etc/acme \
	 $(1)/etc/config \
	 $(1)/etc/init.d \
	 $(1)/usr/share/uacme

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/uacme $(1)/usr/sbin/uacme
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/uacme/uacme.sh $(1)/usr/share/uacme/
	$(SED) '/^CHALLENGE_PATH=/d' $(1)/usr/share/uacme/uacme.sh
	$(INSTALL_CONF) ./files/acme.config $(1)/etc/config/acme
	$(INSTALL_BIN) ./files/run.sh $(1)/usr/share/uacme/run-uacme
	$(INSTALL_BIN) ./files/acme.init $(1)/etc/init.d/acme
endef

define Package/uacme-ualpn/install
	$(INSTALL_DIR) \
	 $(1)/usr/sbin \
	 $(1)/usr/share/uacme

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ualpn $(1)/usr/sbin/ualpn
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ualpn.sh $(1)/usr/share/uacme/
endef

define Package/uacme/prerm
#!/bin/sh
sed -i '/\/etc\/init\.d\/acme start/d' /etc/crontabs/root
endef

$(eval $(call BuildPackage,uacme))
$(eval $(call BuildPackage,uacme-ualpn))

#
# Copyright (C) 2016 - 2020  Stijn Tintel <stijn@linux-ipv6.be>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=domoticz
PKG_VERSION:=2023.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/domoticz/domoticz/tar.gz/$(PKG_VERSION)?
PKG_HASH:=32bcf49df8c80c470352e63004a82d9601b90ccf406096099656250a4515ac28

PKG_MAINTAINER:=David Woodhouse <dwmw2@infradead.org>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=License.txt
PKG_CPE_ID:=cpe:/a:domoticz:domoticz

PKG_BUILD_DEPENDS:=python3 minizip cereal
PKG_BUILD_FLAGS:=no-mips16 lto

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/domoticz
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Open Source Home Automation System
  URL:=http://domoticz.com/
  USERID:=domoticz=6144:domoticz=6144
  DEPENDS:= \
	+boost \
	+boost-date_time \
	+boost-system \
	+boost-thread \
	+jsoncpp \
	+libcurl \
	+python3 \
	+minizip \
	+lua5.3 \
	+libfmt \
	+libmosquitto \
	+libopenssl \
	+libopenzwave \
	+libsqlite3 \
	+libstdcpp \
	+telldus-core \
	+zlib
endef

define Package/domoticz/description
  Domoticz is a Home Automation System that lets you monitor and configure various devices like: Lights, Switches, various sensors/meters like Temperature, Rain, Wind, UV, Electra, Gas, Water and much more. Notifications/Alerts can be sent to any mobile device.
endef

CMAKE_OPTIONS += \
	-DBUILD_SHARED_LIBS=yes \
	-DBoost_NO_BOOST_CMAKE=yes \
	-DGIT_SUBMODULE=no \
	-DCMAKE_BUILD_TYPE=Release \
	-DUSE_BUILTIN_MQTT=no \
	-DUSE_BUILTIN_SQLITE=no \
	-DUSE_BUILTIN_JSONCPP=no \
	-DUSE_BUILTIN_MINIZIP=no \
	-DUSE_BUILTIN_LIBFMT=no \
	-DUSE_LUA_STATIC=no \
	-DUSE_STATIC_BOOST=no \
	-DUSE_STATIC_LIBSTDCXX=no \
	-DUSE_STATIC_OPENZWAVE=no \
	-DUSE_OPENSSL_STATIC=no \
	-DUSE_PYTHON=yes \
	-DWITH_LIBUSB=no

TARGET_CXXFLAGS += -DWITH_GPIO

define Build/Prepare
	$(call Build/Prepare/Default)
	# Remove unwanted scripts
	cd $(PKG_BUILD_DIR)/scripts && rm -rf \
		buienradar_rain_example.pl \
		_domoticz_main* \
		download_update.sh \
		dzVents/{.gitignore,documentation,examples,generated_scripts,data} \
		dzVents/runtime/{integration-tests,misc/smoothing.xlsx,tests} \
		logrotate/ \
		lua_parsers/example* \
		lua/*demo.lua \
		python/ \
		readme.txt \
		restart_domoticz \
		templates/All.Python \
		update_domoticz \
		domoticz.conf
	# Remove *.md
	cd $(PKG_BUILD_DIR) && $(FIND) -name '*.md' -delete
endef

define Package/domoticz/install
	$(INSTALL_DIR) $(1)/etc/config $(1)/etc/hotplug.d/tty $(1)/etc/init.d $(1)/etc/domoticz/plugins
	$(INSTALL_BIN) ./files/domoticz.hotplug $(1)/etc/hotplug.d/tty/domoticz
	$(INSTALL_BIN) ./files/domoticz.init $(1)/etc/init.d/domoticz
	$(INSTALL_CONF) ./files/domoticz.config $(1)/etc/config/domoticz
	$(INSTALL_DIR) $(1)/usr/share/domoticz $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/dzVents $(1)/usr/share/domoticz/dzVents
	$(CP) $(PKG_INSTALL_DIR)/usr/Config $(1)/usr/share/domoticz/Config
	$(CP) $(PKG_INSTALL_DIR)/usr/scripts $(1)/etc/domoticz/scripts
	ln -sf /var/lib/domoticz/dzVents/generated_scripts $(1)/etc/domoticz/scripts/dzVents
	ln -sf /var/lib/domoticz/dzVents/data $(1)/etc/domoticz/scripts/dzVents
	$(CP) $(PKG_INSTALL_DIR)/usr/www $(1)/usr/share/domoticz/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/domoticz $(1)/usr/bin/domoticz
	# compress static web content
	find $(1)/usr/share/domoticz/www -name "*.css" -exec gzip -9 {} \;
	find $(1)/usr/share/domoticz/www -name "*.js" -exec gzip -9 {} \;
	gzip -9 $(1)/usr/share/domoticz/www/*.html
	gzip -9 $(1)/usr/share/domoticz/www/secpanel/*.html
	find $(1)/usr/share/domoticz/www/views -name "*.html" -exec sh -c 'grep -q "<\!--#embed" {} || gzip -9 {}' \;
endef

define Package/domoticz/conffiles
/etc/config/domoticz
/var/lib/domoticz/
/etc/domoticz/
endef

$(eval $(call BuildPackage,domoticz))

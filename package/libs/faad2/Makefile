#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=faad2
PKG_VERSION:=2.11.1
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/knik0/faad2
PKG_MIRROR_HASH:=8dfc89b418293a91c0fc0d11013205449669ce973f5e951500c1e11e3ac61970

PKG_MAINTAINER:=Ted Hess <thess@kitschensync.net>
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:audiocoding:freeware_advanced_audio_decoder_2

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/faad2/Default
  URL:=http://www.audiocoding.com/faad2.html
  TITLE:=Freeware Advanced Audio Decoder
endef

define Package/faad2/Default/description
	FAAD2 is the fastest ISO AAC audio decoder available.
	FAAD2 correctly decodes all MPEG-4 and MPEG-2 MAIN,
	LOW, LTP, LD and ER object type AAC files.
endef

define Package/faad2
$(call Package/faad2/Default)
  SECTION:=sound
  CATEGORY:=Sound
  TITLE+=player
  DEPENDS:=+libfaad2
endef

define Package/faad2/description
$(call Package/faad2/Default/description)
  This package contains a binary to play AAC or MP4 files.
endef

define Package/libfaad2
$(call Package/faad2/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+=library
  MENU:=1
endef

define Package/libfaad2/description
$(call Package/faad2/Default/description)
  This package contains the library.
endef

TARGET_CFLAGS += \
	$(if $(CONFIG_BUILD_PATENTED),,-DLC_ONLY_DECODER -DDISABLE_SBR) \
	$(if $(CONFIG_SOFT_FLOAT),-DFIXED_POINT)

CONFIGURE_ARGS += \
	--without-drm \
	--without-mpeg4ip \
	--without-xmms

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/*.h $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libfaad.so* $(1)/usr/lib/
endef

define Package/faad2/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/faad $(1)/usr/bin/
endef

define Package/libfaad2/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libfaad.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,faad2))
$(eval $(call BuildPackage,libfaad2))

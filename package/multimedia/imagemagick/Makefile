#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imagemagick
PKG_VERSION:=7.1.1.38
PKG_RELEASE:=1
PKG_MAINTAINER:=Aleksey Vasilenko <aleksey.vasilenko@gmail.com>

_PKGVER:=$(basename $(PKG_VERSION))
_PKGREV:=$(_PKGVER)-$(subst .,,$(suffix $(PKG_VERSION)))

PKG_SOURCE:=ImageMagick-$(_PKGREV).tar.xz
PKG_SOURCE_URL:=https://imagemagick.org/archive
PKG_HASH:=48de548d4977fc226c982ca03b9d6ad8001b47d8dc142b49fdca69333bc4ad82
PKG_BUILD_DIR:=$(BUILD_DIR)/ImageMagick-$(_PKGREV)
PKG_FIXUP:=autoreconf

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:imagemagick:imagemagick

PKG_BUILD_FLAGS:=no-mips16 lto
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/imagemagick/Default
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Image manipulation tools
  URL:=https://www.imagemagick.org/
endef

define Package/imagemagick
  $(call Package/imagemagick/Default)
  DEPENDS:=+libltdl +libpthread +zlib +libfreetype +libpng +libjpeg +libtiff +libzip
endef

define Package/imagemagick/description
ImageMagick is a free and open-source software suite for displaying,
converting, and editing raster image and vector image files.
NOTE: this package may not be suitable for many embedded devices because
of its large size. Consider using extroot or alternatively consider
graphicsmagick which is smaller but similar in functionality.
endef

define Package/imagemagick/conffiles
/etc/ImageMagick-7/colors.xml
/etc/ImageMagick-7/delegates.xml
/etc/ImageMagick-7/log.xml
/etc/ImageMagick-7/mime.xml
/etc/ImageMagick-7/policy.xml
/etc/ImageMagick-7/quantization-table.xml
/etc/ImageMagick-7/thresholds.xml
/etc/ImageMagick-7/type-apple.xml
/etc/ImageMagick-7/type-dejavu.xml
/etc/ImageMagick-7/type-ghostscript.xml
/etc/ImageMagick-7/type-urw-base35.xml
/etc/ImageMagick-7/type-windows.xml
/etc/ImageMagick-7/type.xml
endef

CONFIGURE_ARGS += \
	--disable-static \
	--disable-docs \
	--enable-dependency-tracking \
	--with-modules \
	--disable-hdri \
	--with-quantum-depth=8 \
	--disable-cipher \
	--without-bzlib \
	--without-djvu \
	--without-fontconfig \
	--without-gvc \
	--without-heic \
	--without-jbig \
	--without-lcms \
	--without-lqr \
	--without-lzma \
	--without-magick-plus-plus \
	--without-openexr \
	--without-openjp2 \
	--without-raqm \
	--without-raw \
	--without-webp \
	--without-x \
	--without-zstd \
	--without-pango \
	--without-wmf \
	--without-xml

## Avoid linking with libstdcpp
TARGET_LDFLAGS+= -Wl,--as-needed

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/* \
		$(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/*-config \
		$(1)/usr/bin/
	$(SED) 's|prefix=/usr|prefix=$(STAGING_DIR)/usr|' \
		$(1)/usr/bin/*-config
endef

IMlibdir:=usr/lib/ImageMagick-$(_PKGVER)
define Package/imagemagick/install
	$(INSTALL_DIR) $(1)/etc $(1)/usr/bin $(1)/$(IMlibdir)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(RM) $(1)/usr/bin/*-config
	$(CP) $(PKG_INSTALL_DIR)/etc/ImageMagick-* $(1)/etc/
	$(CP) $(PKG_INSTALL_DIR)/$(IMlibdir)/* $(1)/$(IMlibdir)/
endef

$(eval $(call BuildPackage,imagemagick))

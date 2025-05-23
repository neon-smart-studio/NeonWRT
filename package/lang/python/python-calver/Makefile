#
# Copyright (C) 2023 Jeffery To
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-calver
PKG_VERSION:=2022.6.26
PKG_RELEASE:=1

PYPI_NAME:=calver
PKG_HASH:=e05493a3b17517ef1748fbe610da11f10485faa7c416b9d33fd4a52d74894f8b

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Jeffery To <jeffery.to@gmail.com>

PKG_HOST_ONLY:=1
HOST_BUILD_DEPENDS:=python3/host python-build/host python-installer/host python-wheel/host

include ../pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include ../python3-package.mk
include ../python3-host-build.mk

define Package/python3-calver
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Setuptools extension for CalVer package versions
  URL:=https://github.com/di/calver
  DEPENDS:=+python3-light
  BUILDONLY:=1
endef

define Package/python3-calver/description
The calver package is a setuptools extension for automatically defining
your Python package version as a calendar version.
endef

$(eval $(call Py3Package,python3-calver))
$(eval $(call BuildPackage,python3-calver))
$(eval $(call BuildPackage,python3-calver-src))
$(eval $(call HostBuild))

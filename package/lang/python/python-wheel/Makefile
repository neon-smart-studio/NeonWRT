#
# Copyright (C) 2023 Jeffery To
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-wheel
PKG_VERSION:=0.42.0
PKG_RELEASE:=1

PYPI_NAME:=wheel
PKG_HASH:=c45be39f7882c9d34243236f2d63cbd58039e360f85d0913425fbd7ceea617a8

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE.txt
PKG_MAINTAINER:=Jeffery To <jeffery.to@gmail.com>

PKG_HOST_ONLY:=1
HOST_BUILD_DEPENDS:=python3/host python-build/host python-installer/host python-flit-core/host

include ../pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include ../python3-package.mk
include ../python3-host-build.mk

define Package/python3-wheel
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=A built-package format for Python
  URL:=https://github.com/pypa/wheel
  DEPENDS:=+python3-light +python3-email +python3-logging +python3-setuptools
  BUILDONLY:=1
endef

define Package/python3-wheel/description
This library is the reference implementation of the Python wheel
packaging standard, as defined in PEP 427.
endef

$(eval $(call Py3Package,python3-wheel))
$(eval $(call BuildPackage,python3-wheel))
$(eval $(call BuildPackage,python3-wheel-src))
$(eval $(call HostBuild))

#
# Copyright (C) 2015-2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python3-cryptography
PKG_VERSION:=3.4.8
PKG_RELEASE:=2

PYPI_NAME:=cryptography
PKG_MD5SUM:=e8b3e233556690acdc026b432a57c3fa

PKG_LICENSE:=Apache-2.0 BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE.APACHE LICENSE.BSD
PKG_MAINTAINER:=Jeffery To <jeffery.to@gmail.com>

PKG_BUILD_DEPENDS:=libffi/host

HOST_PYTHON3_PACKAGE_BUILD_DEPENDS:=cffi  # cffi>=1.12

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-cryptography
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Cryptographic recipes and primitives
  URL:=https://github.com/pyca/cryptography
  DEPENDS:= \
      +libopenssl \
      +python3-light \
      +python3-email \
      +python3-openssl \
      +python3-urllib \
      +python3-cffi \
      +python3-six
endef

define Package/python3-cryptography/description
cryptography is a package which provides cryptographic recipes and
primitives to Python developers.  Our goal is for it to be your "cryptographic
standard library". It supports Python 2.6-2.7, Python 3.3+, and PyPy 2.6+.
endef

$(eval $(call Py3Package,python3-cryptography))
$(eval $(call BuildPackage,python3-cryptography))
$(eval $(call BuildPackage,python3-cryptography-src))

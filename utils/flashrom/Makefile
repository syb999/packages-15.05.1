#
# Copyright (C) 2010-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=flashrom
PKG_VERSION:=1.2.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-v$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://download.flashrom.org/releases
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-v$(PKG_VERSION)
PKG_MD5SUM:=1482b41efaecc2b5d44bd2ee9466dc73

PKG_MAINTAINER:=Álvaro Fernández Rojas <noltari@gmail.com>
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include flashrom.mk

TARGET_CFLAGS+= \
	-std=gnu89

MAKE_FLAGS+= \
	PREFIX="/usr"

define Package/flashrom/default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=FlashROM Utility
  URL:=https://www.flashrom.org/
endef

define Package/flashrom
  $(Package/flashrom/default)
  TITLE+= (full)
  DEPENDS+= \
    +(TARGET_x86||TARGET_x86_64):dmidecode \
    +libftdi1 \
    +libusb-1.0 \
    +pciutils
  VARIANT:=full
  DEFAULT_VARIANT:=1
endef

define Package/flashrom-pci
  $(Package/flashrom/default)
  TITLE+= (pci)
  DEPENDS+= \
    +(TARGET_x86||TARGET_x86_64):dmidecode \
    +pciutils
  VARIANT:=pci
endef

define Package/flashrom-spi
  $(Package/flashrom/default)
  TITLE+= (spi)
  VARIANT:=spi
endef

define Package/flashrom-usb
  $(Package/flashrom/default)
  TITLE+= (usb)
  DEPENDS+= \
    +libftdi1 \
    +libusb-1.0
  VARIANT:=usb
endef

define Package/flashrom/default/description
 flashrom is an utility for identifying, reading, writing, verifying
 and erasing flash chips. It's often used to flash BIOS/EFI/coreboot
 /firmware images.
endef
Package/flashrom/description = $(Package/flashrom/default/description)
Package/flashrom-pci/description = $(Package/flashrom/default/description)
Package/flashrom-spi/description = $(Package/flashrom/default/description)
Package/flashrom-usb/description = $(Package/flashrom/default/description)

define Package/flashrom/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom
endef
define Package/flashrom-pci/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom-pci
endef
define Package/flashrom-spi/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom-spi
endef
define Package/flashrom-usb/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/flashrom $(1)/usr/sbin/flashrom-usb
endef

$(eval $(call BuildPackage,flashrom))
$(eval $(call BuildPackage,flashrom-pci))
$(eval $(call BuildPackage,flashrom-spi))
$(eval $(call BuildPackage,flashrom-usb))

#
# Copyright (C) 2018-2020 Ruilin Peng (Nick) <pymumu@gmail.com>.
#
# smartdns is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# smartdns is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.
include $(TOPDIR)/rules.mk

PKG_NAME:=smartdns-old

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/pymumu/smartdns.git

PKG_REV:=8973acad44ab94111c4ef8e8325c4dddd38846c8
PKG_VERSION:=1.2020.05.10
PKG_RELEASE:=1
PKG_LICENSE:=GPL-3.0
PKG_MD5SUM:=a0e56060e0a4383651fa9643e504ad39

PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += -std=gnu99

MAKE_ARGS := CFLAGS="$(TARGET_CFLAGS)" CC=$(TARGET_CC)

define Package/smartdns-old
  SECTION:=net
  CATEGORY:=Network
  TITLE:=smartdns server for 64m ram
  URL:=http://github.com/pymumu/smartdns/
  MAINTAINER:=Nick Peng <pymumu@gmail.com>
  DEPENDS:=+libopenssl +libpthread @!TARGET_kirkwood
endef

define Package/smartdns-old/description
SmartDNS is a local DNS server. SmartDNS accepts DNS query requests from local clients, obtains DNS query results from multiple upstream DNS servers, and returns the fastest access results to clients.
endef

define Build/Configure
	mkdir -p $(PKG_INSTALL_DIR)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/src $(MAKE_ARGS) all
endef

define Package/smartdns-old/conffiles
/etc/config/smartdns
/etc/smartdns/address.conf
/etc/smartdns/blacklist-ip.conf
/etc/smartdns/custom.conf
endef

define Package/smartdns-old/install
	$(INSTALL_DIR) $(1)/usr/sbin $(1)/etc/config $(1)/etc/init.d $(1)/etc/smartdns
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/smartdns $(1)/usr/sbin/smartdns
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/package/openwrt/files/etc/init.d/smartdns $(1)/etc/init.d/smartdns
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/package/openwrt/address.conf $(1)/etc/smartdns/address.conf
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/package/openwrt/blacklist-ip.conf $(1)/etc/smartdns/blacklist-ip.conf
	$(INSTALL_CONF) ./custom.conf $(1)/etc/smartdns/custom.conf
	$(INSTALL_CONF) ./self-smartdns.conf $(1)/etc/smartdns/self-smartdns.conf
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/package/openwrt/files/etc/config/smartdns $(1)/etc/config/smartdns
endef

$(eval $(call BuildPackage,smartdns-old))

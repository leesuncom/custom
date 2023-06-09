# SPDX-License-Identifier: GPL-3.0-or-later
#
# Copyright (c) 2018-2023 Nick Peng (pymumu@gmail.com)

include $(TOPDIR)/rules.mk

PKG_NAME:=smartdns
PKG_VERSION:=42
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/pymumu/smartdns/tar.gz/Release$(PKG_VERSION)?
PKG_HASH:=83bb3c588672dff7fe702223538d6e61a4d475e592643a57d1416aade0b363d0
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-Release$(PKG_VERSION)

PKG_MAINTAINER:=Nick Peng <pymumu@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

MAKE_PATH:=src
MAKE_VARS+= VER=$(PKG_VERSION)

define Package/smartdns
  SECTION:=net
  CATEGORY:=Network
  TITLE:=smartdns server
  DEPENDS:=+libpthread +libopenssl
  URL:=https://www.github.com/pymumu/smartdns/
endef

define Package/smartdns/description
SmartDNS is a local DNS server which accepts DNS query requests from local network clients,
gets DNS query results from multiple upstream DNS servers concurrently, and returns the fastest IP to clients.
Unlike dnsmasq's all-servers, smartdns returns the fastest IP, and encrypt DNS queries with DoT or DoH.
endef

define Package/smartdns/conffiles
/etc/smartdns/conf.d/anti-ad-for-smartdns.conf
/etc/smartdns/domain-set/gfw.txt
/etc/smartdns/domain-set/gfwlist_domain.txt
/etc/config/smartdns
/etc/smartdns/address.conf
/etc/smartdns/blacklist-ip.conf
/etc/smartdns/custom.conf
/etc/smartdns/domain-block.list
/etc/smartdns/domain-forwarding.list
/etc/smartdns/up.sh
/etc/smartdns/cn.conf
endef

define Package/smartdns/install
	$(INSTALL_DIR) $(1)/usr/sbin $(1)/etc/config $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/smartdns $(1)/etc/smartdns/domain-set/ $(1)/etc/smartdns/conf.d/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/smartdns $(1)/usr/sbin/smartdns
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/package/openwrt/files/etc/init.d/smartdns $(1)/etc/init.d/smartdns
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/package/openwrt/address.conf $(1)/etc/smartdns/address.conf
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/package/openwrt/blacklist-ip.conf $(1)/etc/smartdns/blacklist-ip.conf
	$(INSTALL_CONF) $(CURDIR)/conf/custom.conf $(1)/etc/smartdns/custom.conf
	$(INSTALL_CONF) $(CURDIR)/conf/smartdns.conf $(1)/etc/config/smartdns
	$(INSTALL_CONF) $(CURDIR)/conf/up.sh $(1)/etc/smartdns/up.sh
	$(INSTALL_CONF) $(CURDIR)/conf/cn.conf $(1)/etc/smartdns/cn.conf
	$(INSTALL_CONF) $(CURDIR)/conf/domain-forwarding.list $(1)/etc/smartdns/domain-forwarding.list
	$(INSTALL_CONF) $(CURDIR)/conf/domain-block.list $(1)/etc/smartdns/domain-block.list
	$(INSTALL_CONF) $(CURDIR)/conf/conf.d/anti-ad-for-smartdns.conf $(1)/etc/smartdns/conf.d/anti-ad-for-smartdns.conf
	$(INSTALL_CONF) $(CURDIR)/conf/domain-set/gfw.txt $(1)/etc/smartdns/domain-set/gfw.txt
	$(INSTALL_CONF) $(CURDIR)/conf/domain-set/gfwlist_domain.txt $(1)/etc/smartdns/domain-set/gfwlist_domain.txt
endef

$(eval $(call BuildPackage,smartdns))

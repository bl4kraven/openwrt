#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.


include $(TOPDIR)/rules.mk

PKG_NAME:=n2n
PKG_RELEASE:=1.3.2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/meyerd/n2n
PKG_SOURCE_VERSION:=d8d1257

include $(INCLUDE_DIR)/package.mk

define Build/Prepare
	$(call Build/Prepare/Default,)
	$(CP) ./files $(PKG_BUILD_DIR)/
endef

define Package/n2n
  SECTION:=net
  CATEGORY:=Network
  TITLE:=VPN tunneling daemon
  DEPENDS:=+libpthread +kmod-tun
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/n2n_v1 $(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)" LDFLAGS="$(TARGET_LDFLAGS)" INSTALL_PROG=":"
endef

define Package/n2n/install
	$(CP) $(PKG_BUILD_DIR)/files/*  $(1)/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/n2n_v1/edge $(1)/usr/sbin/
	find $(1) -type d | $(XARGS) chmod 0755
endef

$(eval $(call BuildPackage,n2n))

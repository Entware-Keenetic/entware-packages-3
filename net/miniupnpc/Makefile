#
# Copyright (C) 2010-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=miniupnpc
PKG_VERSION:=2.0.20170509
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://miniupnp.free.fr/files
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=d3c368627f5cdfb66d3ebd64ca39ba54d6ff14a61966dbecb8dd296b7039f16a
PKG_MAINTAINER:=Steven Barth <cyrus@openwrt.org>

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/miniupnpc/Default
  TITLE:=Lightweight UPnP
  URL:=http://miniupnp.tuxfamily.org/
endef

define Package/miniupnpc
  $(call Package/miniupnpc/Default)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  TITLE+= client
  DEPENDS:=+libminiupnpc
endef

define Package/libminiupnpc
  $(call Package/miniupnpc/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+= library
endef

TARGET_CFLAGS += $(FPIC)

MAKE_FLAGS += \
	OS="Linux" \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/miniupnpc
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/include/miniupnpc/*.h \
		$(1)/opt/include/miniupnpc/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/*.{so*,a} \
		$(1)/opt/lib/
endef

define Package/miniupnpc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/upnpc $(1)/opt/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/listdevices $(1)/opt/bin/
endef

define Package/libminiupnpc/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/lib/libminiupnpc.so.* \
		$(1)/opt/lib/
endef

$(eval $(call BuildPackage,miniupnpc))
$(eval $(call BuildPackage,libminiupnpc))

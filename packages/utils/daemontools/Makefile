#
# Copyright (C) 2007 OpenWrt.org
# Original port by FreeWRT project. 
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Alexander Tsvyashchenko	Created OpenWRT package as per Trac ticket 2497
#

include $(TOPDIR)/rules.mk

PKG_NAME:=daemontools
PKG_VERSION:=0.76
PKG_RELEASE:=1

PKG_SOURCE:=${PKG_NAME}-${PKG_VERSION}.tar.gz
PKG_SOURCE_URL:=http://cr.yp.to/daemontools/
PKG_MD5SUM:=1871af2453d6e464034968a0fbcb2bfc

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

PKG_UNPACK += && mv $(PKG_BUILD_DIR)/../admin/* $(PKG_BUILD_DIR)/.. && rmdir $(PKG_BUILD_DIR)/../admin

define Package/daemontools
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=
  TITLE:=Tools for managing UNIX services
  URL:=http://cr.yp.to/daemontools.html
endef

define Package/daemontools/description
	Daemontools is a collection of tools for managing UNIX services by DJ Bernstein.
endef

define Build/Compile
	cd $(PKG_BUILD_DIR) && \
	TARGET_CC="$(TARGET_CC)" \
	TARGET_CFLAGS="$(TARGET_CFLAGS)" \
	TARGET_LDFLAGS="$(TARGET_LDFLAGS)" \
	$(PKG_BUILD_DIR)/package/compile
endef

define Package/daemontools/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/command/* $(1)/usr/bin
endef

$(eval $(call BuildPackage,daemontools))


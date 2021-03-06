#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bluez-utils
PKG_VERSION:=3.36
PKG_RELEASE:=6

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://bluez.sourceforge.net/download
PKG_MD5SUM:=4fc292b635ba7b442c7aaf5680199012

include $(INCLUDE_DIR)/package.mk

define Package/bluez-utils
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+bluez-libs +libpthread +dbus +libintl +libiconv
  TITLE:=Bluetooth utilities
  URL:=http://www.bluez.org/
endef

define Package/bluez-utils/conffiles
/etc/bluetooth/hcid.conf
/etc/bluetooth/rfcomm.conf
/etc/config/bluetooth
endef

CONFIGURE_ARGS += \
	--disable-glib \
	--enable-pand \
	--enable-rfcomm \
	--enable-dund \
	--enable-serial \
	--enable-network \
	--enable-usb \
	--enable-input \
	--disable-audio \
	--with-bluez="$(STAGING_DIR)/usr/include" \
	--with-usb=yes \

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		LDFLAGS="$(TARGET_LDFLAGS) \
			-L$(STAGING_DIR)/usr/lib/libintl/lib \
			-L$(STAGING_DIR)/usr/lib/libiconv/lib" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

#copy bluetooth.conf nach /etc/dbus-1/system.d/

define Package/bluez-utils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/* $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/bluetooth
	$(CP) $(PKG_INSTALL_DIR)/../hcid/hcid.conf $(1)/etc/bluetooth/
	$(CP) $(PKG_INSTALL_DIR)/../rfcomm/rfcomm.conf $(1)/etc/bluetooth/
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/bluetooth.conf $(1)/etc/config/bluetooth
	$(INSTALL_DIR) $(1)/etc/dbus-1/system.d/
	$(INSTALL_DATA) ./files/bluetooth.dbus $(1)/etc/dbus-1/system.d/bluetooth.conf
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/bluez-utils.init $(1)/etc/init.d/bluez-utils
endef

$(eval $(call BuildPackage,bluez-utils))

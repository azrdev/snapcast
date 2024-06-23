#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME := snapclient
PKG_VERSION := 0.28.0
PKG_RELEASE := 1
PKG_USE_MIPS16 := 0

PKG_BUILD_DIR:=$(BUILD_DIR)/snapcast-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += -DBUILD_TESTS=OFF

define Package/snapclient
	SECTION := sound
	CATEGORY := Sound
	URL := https://github.com/badaix/snapcast
	TITLE := Synchronous multiroom audio player Snapclient
	DEPENDS := +AUDIO_SUPPORT:alsa-lib +libstdcpp +libavahi-client +libatomic +libogg +libflac +libopus +boost +libsoxr +libvorbisidec +libsoxr

	DEFAULT := y
endef

define Package/snapclient/description
	Synchronous audio player
	Snapcast client
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./* $(PKG_BUILD_DIR)/
endef

define Package/snapclient/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/snapclient $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/snapclient.init $(1)/etc/init.d/snapclient
	$(INSTALL_DIR) $(1)/etc/default
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/extras/package/debian/snapclient.default $(1)/etc/default/snapclient
endef

$(eval $(call BuildPackage,snapclient))


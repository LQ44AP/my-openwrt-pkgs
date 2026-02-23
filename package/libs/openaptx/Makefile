include $(TOPDIR)/rules.mk

PKG_NAME:=openaptx
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/arkq/openaptx.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=skip

include $(INCLUDE_DIR)/package.mk

define Package/openaptx
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Open source aptX codec library
  DEPENDS:=+libsndfile
endef

define Build/Configure
	# openaptx 使用简单 Makefile，通常不需要 ./configure
endef

define Package/openaptx/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libopenaptx.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,openaptx))
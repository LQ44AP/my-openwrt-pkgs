include $(TOPDIR)/rules.mk

PKG_NAME:=libldac
PKG_VERSION:=2.0.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/EHfive/ldacBT.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=skip

PKG_MAINTAINER:=Sony Corporation
PKG_LICENSE:=Apache-2.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libldac
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Sony LDAC library
  URL:=https://github.com/EHfive/ldacBT
  DEPENDS:=@(arm||aarch64||x86_64)
endef

define Package/libldac/description
  Sony LDAC Bluetooth codec library (AOSP version).
endef

CMAKE_OPTIONS += \
	-DINSTALL_LIBDIR=/usr/lib \
	-DLDAC_SOFT_FLOAT=OFF

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/ldac
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ldac/*.h $(1)/usr/include/ldac/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libldacBT*.so* $(1)/usr/lib/
endef

define Package/libldac/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libldacBT*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libldac))

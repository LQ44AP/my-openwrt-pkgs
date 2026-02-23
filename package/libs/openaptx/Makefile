include $(TOPDIR)/rules.mk

PKG_NAME:=openaptx
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/arkq/openaptx.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=skip

# 关键：引入 cmake 编译支持
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/openaptx
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Open source aptX codec library
  DEPENDS:=+libsndfile
endef

# CMake 宏会自动处理 Build/Configure 和 Build/Compile
# 我们只需要定义安装逻辑

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/*.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libopenaptx.so* $(1)/usr/lib/
endef

define Package/openaptx/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libopenaptx.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,openaptx))

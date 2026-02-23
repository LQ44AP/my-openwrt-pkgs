include $(TOPDIR)/rules.mk

PKG_NAME:=openaptx
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/arkq/openaptx.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=skip

# 告诉系统在临时目录进行安装，以便后续拷贝
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/openaptx
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Open source aptX codec library
  DEPENDS:=+libsndfile
endef

# 关键修正：通过 CMake 参数关闭示例程序的编译，避免交叉编译冲突
CMAKE_OPTIONS += -DWITH_SAMPLES=OFF

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

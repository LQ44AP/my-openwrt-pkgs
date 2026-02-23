include $(TOPDIR)/rules.mk

PKG_NAME:=openaptx
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/arkq/openaptx.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=skip

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/openaptx
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Open source aptX codec library
  DEPENDS:=+libsndfile
endef

# 核心补丁：通过配置选项禁用 SAMPLES 和 UTILS
# 这通常是防止交叉编译时运行目标二进制文件的标准做法
CMAKE_OPTIONS += \
	-DWITH_SAMPLES=OFF \
	-DWITH_UTILS=OFF

# 如果上面的选项不起作用，强制在准备阶段删除导致问题的代码行
define Build/Prepare
	$(call Build/Prepare/Default)
	$(SED) '/add_subdirectory(src)/d' $(PKG_BUILD_DIR)/CMakeLists.txt
	# 确保 lib 目录被正常处理，我们可以手动添加
	echo "add_subdirectory(lib)" >> $(PKG_BUILD_DIR)/CMakeLists.txt
endef

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

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

# 1. 禁用不需要的选项
CMAKE_OPTIONS += \
	-DWITH_SAMPLES=OFF \
	-DWITH_UTILS=OFF

# 2. 核心补丁：精准移除 src/CMakeLists.txt 中关于 sample 和 bin2array 的定义
# 这样 CMake 就只会编译 libopenaptx.so，而不会去跑那个报错的 bin2array
define Build/Prepare
	$(call Build/Prepare/Default)
	# 进入源码目录
	(cd $(PKG_BUILD_DIR)/src; \
	 $(SED) '/add_executable(bin2array/d' CMakeLists.txt; \
	 $(SED) '/target_link_libraries(bin2array/d' CMakeLists.txt; \
	 $(SED) '/add_custom_command/,/DEPENDS bin2array/d' CMakeLists.txt; \
	 $(SED) '/set(SAMPLES_SRC/,/)/d' CMakeLists.txt; \
	)
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

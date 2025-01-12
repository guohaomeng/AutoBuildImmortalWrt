include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

# 定义驱动包信息
PKG_NAME:=uwe5622-wifi
PKG_VERSION:=1.0
PKG_RELEASE:=1

# 定义驱动源码路径
# PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
# PKG_SOURCE_URL:=file:///path/to/uwe5622_driver
# PKG_HASH:=your_source_hash

# 包含 OpenWrt 的包定义规则
include $(INCLUDE_DIR)/package.mk

# 定义驱动模块的包信息
define KernelPackage/uwe5622-wifi
  SUBMENU:=Wireless Drivers
  TITLE:=Driver for Unisoc UWE5622 WiFi chip
  DEPENDS:=@TARGET_sunxi
  FILES:=$(PKG_BUILD_DIR)/unisocwifi/unisocwifi.ko
  AUTOLOAD:=$(call AutoLoad,50,unisocwifi)
endef

# 定义驱动的编译规则
define Build/Compile
  $(MAKE) -C "$(LINUX_DIR)" \
    ARCH="$(LINUX_KARCH)" \
    CROSS_COMPILE="$(TARGET_CROSS)" \
    M="$(PKG_BUILD_DIR)" \
    modules
endef

# 定义驱动的安装规则
define KernelPackage/uwe5622-wifi/install
  $(INSTALL_DIR) $(1)/lib/firmware/uwe5622/
  $(INSTALL_DATA) $(PKG_BUILD_DIR)/firmware/* $(1)/lib/firmware/uwe5622/
endef

# 生成 OpenWrt 包
$(eval $(call KernelPackage,uwe5622-wifi))
include $(TOPDIR)/rules.mk

PKG_NAME:=shadowsocks-libev
PKG_VERSION:=1.4.7
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/madeye/shadowsocks-libev.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=d37f8d302532a8d442233d9b752324ffff99bbd0
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_MAINTAINER:=Max Lv <max.c.lv@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/shadowsocks-libev/Default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Lightweight Secured Socks5 Proxy
  URL:=https://github.com/madeye/shadowsocks-libev
endef

define Package/shadowsocks-libev
  $(call Package/shadowsocks-libev/Default)
  TITLE+= (OpenSSL)
  VARIANT:=openssl
  DEPENDS:=+libopenssl
endef

define Package/shadowsocks-libev-polarssl
  $(call Package/shadowsocks-libev/Default)
  TITLE+= (PolarSSL)
  VARIANT:=polarssl
  DEPENDS:=+libpolarssl
endef

define Package/shadowsocks-libev/description
Shadowsocks-libev is a lightweight secured scoks5 proxy for embedded devices and low end boxes.
endef

Package/shadowsocks-libev-polarssl/description=$(Package/shadowsocks-libev/description)

ifeq ($(BUILD_VARIANT),polarssl)
        CONFIGURE_ARGS += --with-crypto-library=polarssl
endif

define Package/shadowsocks-libev/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ss-{local,redir,tunnel} $(1)/usr/bin
endef

Package/shadowsocks-libev-polarssl/install=$(Package/shadowsocks-libev/install)

$(eval $(call BuildPackage,shadowsocks-libev))
$(eval $(call BuildPackage,shadowsocks-libev-polarssl))

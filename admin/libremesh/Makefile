include $(TOPDIR)/rules.mk

PKG_NAME:=lime-system
PKG_VERSION=2019-03-14-1552588427
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/libremesh/lime-packages.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=7af7f0506bcc00286db4cf1f6d1ff207ccf5c4ef
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_LICENSE:=GPL-3.0
PKGARCH:=all

LIME_ID:=LiMe
LIME_RELEASE:=$(shell git branch | sed -n '/\* /s///p')
LIME_CODENAME:=development
LIME_BRANCH:=$(shell git branch | sed -n '/\* /s///p')
LIME_REVISION:=$(shell git log -n 1 --pretty=%h)
LIME_BUILDDATE:=$(shell date +%Y%m%d_%H%M)
LIME_DESCRIPTION:=$(LIME_ID) $(LIME_RELEASE) $(LIME_CODENAME) ($(LIME_BRANCH) rev. $(LIME_REVISION) $(LIME_BUILDDATE))

include $(INCLUDE_DIR)/package.mk

define Package/lime-system
  TITLE:=libremesh system files
  CATEGORY:=Administration
  SECTION:=admin
  SUBMENU:=LibreMesh
  MAINTAINER:=Gui Iribarren <gui@altermundi.net>
  URL:=https://libremesh.org
  DEPENDS:=+libiwinfo-lua +lua +libuci-lua +luci-lib-ip +luci-lib-nixio
  PKGARCH:=all
endef

define Package/lime-system/description
	Basic system files for LiMe node
endef

define Package/lime-system/conffiles
	/etc/config/lime
	/etc/config/lime-defaults
endef

define Build/Compile
endef

LIME_VERSION_SED:=$(SED)   's,%LIME_ID%,$(LIME_ID),g' \
			-e 's,%LIME_RELEASE%,$(LIME_RELEASE),g' \
			-e 's,%LIME_CODENAME%,$(LIME_CODENAME),g' \
			-e 's,%LIME_BRANCH%,$(LIME_BRANCH),g' \
			-e 's,%LIME_REVISION%,$(LIME_REVISION),g' \
			-e 's,%LIME_BUILDDATE%,$(LIME_BUILDDATE),g' \
			-e 's,%LIME_DESCRIPTION%,$(LIME_DESCRIPTION),g'

define Package/lime-system/install
	$(INSTALL_DIR) $(1)/
	$(CP) ./packages/lime-system/files/* $(1)/
	$(LIME_VERSION_SED) \
		$(1)/etc/lime_release \
		$(1)/etc/uci-defaults/90_lime-banner
endef

define Package/lime-system/postinst
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || /etc/init.d/firewall-lime enable || true
endef

$(eval $(call BuildPackage,lime-system))

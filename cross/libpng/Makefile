PKG_NAME = libpng
PKG_VERS = 1.6.38
PKG_EXT = tar.xz
PKG_DIST_NAME = $(PKG_NAME)-$(PKG_VERS).$(PKG_EXT)
PKG_DIST_SITE = https://download.sourceforge.net/libpng
PKG_DIR = $(PKG_NAME)-$(PKG_VERS)

DEPENDS = cross/zlib

HOMEPAGE = http://www.libpng.org/pub/png/libpng.html
COMMENT  = Portable Network Graphics Library
LICENSE  = http://www.libpng.org/pub/png/src/libpng-LICENSE.txt

GNU_CONFIGURE = 1
CONFIGURE_ARGS = --disable-static
ADDITIONAL_CFLAGS = -O

include ../../mk/spksrc.cross-cc.mk

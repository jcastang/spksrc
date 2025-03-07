SPK_NAME = synocli-file
SPK_VERS = 2.7
SPK_REV = 20
SPK_ICON = src/synocli-file.png

# packages depending on cross/zlib must be defined later, see below
DEPENDS = cross/less cross/tree cross/ncdu cross/jdupes cross/rhash cross/nano cross/file
DEPENDS += cross/detox
DEPENDS += cross/lzip cross/plzip
DEPENDS += cross/mg
DEPENDS += cross/jupp
DEPENDS += cross/iconv
DEPENDS += cross/dos2unix

OPTIONAL_DEPENDS  = cross/rmlint cross/rnm cross/micro cross/fzf cross/ripgrep cross/fd cross/sd
OPTIONAL_DEPENDS += cross/bat cross/exa
OPTIONAL_DEPENDS += cross/nnn cross/nnn_4.0

MAINTAINER = hgy59
DISPLAY_NAME = SynoCli File Tools

POST_STRIP_TARGET = synocli-file_extra_install

OPTIONAL_DESC =

include ../../mk/spksrc.common.mk

ifneq ($(findstring $(ARCH),$(OLD_PPC_ARCHS)),$(ARCH))
# build rust tools before packages depending on cross/zlib
# These tools must use cross/zlib-ng instead of cross/zlib, otherwise will fail to find zlib (x64 only)
DEPENDS += cross/bat cross/exa
OPTIONAL_DESC := $(OPTIONAL_DESC)", bat, exa"
endif

# PPC archs except QorIQ
ifneq ($(findstring $(ARCH),$(OLD_PPC_ARCHS)),$(ARCH))
# rmlint must be built before "cross/mc cross/pcre2 cross/fdupes cross/zstd"
# to use libblkid and support reflink
DEPENDS += cross/rmlint
OPTIONAL_DESC := $(OPTIONAL_DESC)", rmlint"
endif

# packages depending on cross/zlib
DEPENDS += cross/mc cross/pcre2 cross/fdupes cross/zstd

ifneq ($(findstring $(ARCH),$(OLD_PPC_ARCHS) $(ARMv5_ARCHS)),$(ARCH))
# gcc with stdc++11 support
ifneq ($(call version_lt, ${TCVERSION}, 6.0)$(call version_ge, ${TCVERSION}, 3.0),11)
# to build rnm, GCC >= 4.8 is required
DEPENDS += cross/rnm
OPTIONAL_DESC := $(OPTIONAL_DESC)", rnm"
endif
endif

ifneq ($(findstring $(ARCH),$(OLD_PPC_ARCHS)),$(ARCH))
OPTIONAL_DESC := $(OPTIONAL_DESC)", nnn (n³)"
ifeq ($(call version_ge, ${TCVERSION}, 7.0),1)
ifneq ($(findstring $(ARCH),comcerto2k),$(ARCH))
DEPENDS += cross/nnn
else
# comcerto2k for DSM>=7
DEPENDS += cross/nnn_4.0
endif
else ifneq ($(findstring $(ARCH),$(32bit_ARCHS)),$(ARCH))
DEPENDS += cross/nnn
else
# 32-bit archs for DSM<7
DEPENDS += cross/nnn_4.0
endif
endif

# PPC archs are not supported with golang
ifneq ($(findstring $(ARCH),$(PPC_ARCHS)),$(ARCH))
DEPENDS += cross/micro cross/fzf
OPTIONAL_DESC := $(OPTIONAL_DESC)", micro (editor), fzf (fuzzy finder)"
endif

ifneq ($(findstring $(ARCH),$(OLD_PPC_ARCHS)),$(ARCH))
DEPENDS += cross/ripgrep
OPTIONAL_DESC := $(OPTIONAL_DESC)", rg (ripgrep)"
DEPENDS += cross/fd
OPTIONAL_DESC := $(OPTIONAL_DESC)", fd (fd-find)"
DEPENDS += cross/sd
OPTIONAL_DESC := $(OPTIONAL_DESC)", sd (sed alternative)"
endif

# activate additional features for pcre2grep and pcre2test
PCRE2_CLI_FULL = 1
export PCRE2_CLI_FULL

DESCRIPTION = "SynoCli File Tools provide a set of small command-line utilities: less, tree, ncdu, jdupes, fdupes, rhash, mc \(midnight commander\), mg \(emacs-like text editor\), nano, jupp \(based on JOE - Joe\'s Own Editor 3.1\), file, detox, pcre2, zstd, lzip, plzip, detox, iconv, dos2unix tools$(OPTIONAL_DESC)."
STARTABLE = no
CHANGELOG = "1. Update bat to v0.23.0.<br/>2. Update dos2unix to v7.5.0.<br/>3. Update fzf to v0.40.0.<br/>4. Update gdu to v5.23.0.<br/>5. Update jdupes to v1.26.1.<br/>6. Update jupp to v3.1-41.<br/>7. Update less to v633.<br/>8. Update mc to v4.8.29.<br/>9. Update mg to v3.6.<br/>10. Update nano to v7.2.<br/>11. Update ncdu to v1.18.1.<br/>12. Update nnn to v.4.8, but downgrade nnn to v4.0 for 32-bit archs on DSM<7.<br/>13. Update pcre2 to v10.42.<br/>14. Update tree to v2.1.0."

SERVICE_SETUP = src/service-setup.sh

HOMEPAGE = https://github.com/SynoCommunity/spksrc/wiki/FAQ-SynoCliFile
LICENSE  = Each tool is licensed under it's respective license.

SPK_COMMANDS  = bin/less bin/lessecho bin/lesskey
SPK_COMMANDS += bin/tree
SPK_COMMANDS += bin/ncdu
SPK_COMMANDS += bin/jdupes
SPK_COMMANDS += bin/mc bin/mcdiff bin/mcview bin/mcedit
SPK_COMMANDS += bin/nano bin/rnano
SPK_COMMANDS += bin/file
SPK_COMMANDS += bin/detox
SPK_COMMANDS += bin/pcre2grep bin/pcre2test
SPK_COMMANDS += bin/rmlint
SPK_COMMANDS += bin/rnm
SPK_COMMANDS += bin/zstd bin/unzstd bin/zstdcat bin/zstdmt bin/zstdgrep bin/zstdless
SPK_COMMANDS += bin/lzip bin/plzip
SPK_COMMANDS += bin/fdupes
SPK_COMMANDS += bin/micro
SPK_COMMANDS += bin/fzf
SPK_COMMANDS += bin/rg
SPK_COMMANDS += bin/fd
SPK_COMMANDS += bin/sd
SPK_COMMANDS += bin/mg
SPK_COMMANDS += bin/bat
SPK_COMMANDS += bin/exa
SPK_COMMANDS += bin/jmacs bin/joe bin/jpico bin/jstar bin/jupp bin/rjoe
SPK_COMMANDS += bin/nnn
SPK_COMMANDS += bin/iconv
SPK_COMMANDS += bin/dos2unix bin/unix2dos bin/mac2unix bin/unix2mac

SPK_COMMANDS += bin/rhash
SPK_COMMANDS += bin/ed2k-link
SPK_COMMANDS += bin/edonr256-hash
SPK_COMMANDS += bin/edonr512-hash
SPK_COMMANDS += bin/gost12-256-hash
SPK_COMMANDS += bin/gost12-512-hash
SPK_COMMANDS += bin/has160-hash
SPK_COMMANDS += bin/magnet-link
SPK_COMMANDS += bin/sfv-hash
SPK_COMMANDS += bin/tiger-hash
SPK_COMMANDS += bin/tth-hash
SPK_COMMANDS += bin/whirlpool-hash

include ../../mk/spksrc.spk.mk

.PHONY: synocli-file_extra_install
synocli-file_extra_install:
	@$(MSG) "Set library runpath in rhash executable."
	@patchelf --set-rpath /var/packages/$(SPK_NAME)/target/lib $(STAGING_DIR)/bin/rhash
